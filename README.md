# PaketMerge
move paket references from one directory to another identical directory



using System;
using System.Collections.Generic;
using System.Linq;
using Microsoft.VisualStudio.TestTools.UnitTesting;
namespace paketmover
{
    [TestClass]
    public class UnitTest1
    {
        [TestMethod]
        public void TestMethod1()
        {
            const string sourceDir = @"D:\source";
            const string destDir = @"D:\destination";

            var sources = System.IO.Directory.GetDirectories(sourceDir).ToList();
            var work= (from source in sources
                       let sourceFolder = source.Replace(sourceDir, "")
                       let sourcePaket = source + "\\" + "paket.references"
                       where System.IO.File.Exists(sourcePaket)
                       let destPaket = destDir + sourceFolder + "\\" + "paket.references"
                       select new Tuple<string, string>(sourcePaket, destPaket)).ToList();

            work.ForEach(w => System.IO.File.WriteAllText(w.Item2, System.IO.File.ReadAllText(w.Item1)));

        }
    }
}
