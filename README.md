# ANLY580-90-2016
Special Topics: Data Visualization

This is a GitHub repo for use in my class.  We are working on building familiarity and experience with social coding tools. 

https://mdsservices.dealogic.com/Router/MDS/1/ChangeStore/Change/Latest 

http://tesdevweb:8080/api/tes-6.2/post


            string result = web.DownloadString("http://eoddata.com/stockquote/NYSE/A.htm");

            string result2 = web.DownloadString("https://finance.yahoo.com/quote/AAPL/key-statistics?p=AAPL");

            var doc = new HtmlDocument();

            doc.LoadHtml(result);

            var feve = doc.GetElementbyId("ctl00_cph1_divFundamentals").InnerText.Split('\n');

            StockX sX = new StockX(feve);
            
                    class StockX
        {
            public string Sector { get; set; }
            public string Industry { get; set; }
            public string Shares { get; set; }
            public string MarketCap { get; set; }


            public StockX()
            {


            }

            public StockX(string[] f)
            {

                Sector = f.Where(s => s.Contains("Sector")).Select(s => s).Single().Split(':')[1];
                Industry = f.Where(s => s.Contains("Industry")).Select(s => s).Single().Split(':')[1];
                Shares = f.Where(s => s.Contains("Shares")).Select(s => s).Single().Split(':')[1];
                MarketCap = f.Where(s => s.Contains("Market Cap")).Select(s => s).Single().Split(':')[1];

                if (Shares.Contains("M"))
                {
                    Shares = (decimal.Parse(Shares.Replace('M', ' ')) * 1000000).ToString();
                }
                else if (Shares.Contains("B"))
                {
                    Shares = (decimal.Parse(Shares.Replace('B', ' ')) * 1000000000).ToString();
                }

                if (MarketCap.Contains("M"))
                {
                    MarketCap = (decimal.Parse(MarketCap.Replace('M', ' ')) * 1000000).ToString();
                }
                else if (MarketCap.Contains("B"))
                {
                    MarketCap = (decimal.Parse(MarketCap.Replace('B', ' ')) * 1000000000).ToString();
                }

                Console.WriteLine(Sector);
                Console.WriteLine(Industry);
                Console.WriteLine(Shares);
                Console.WriteLine(MarketCap);

            }

        }
