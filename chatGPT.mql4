// Define input parameters
input int fastPeriod = 10;   // Fast moving average period
input int slowPeriod = 20;   // Slow moving average period
input double lotSize = 0.01;  // Trading lot size

// Define global variables
int maCrossSignal = 0;       // Signal for moving average crossover

//+------------------------------------------------------------------+
//| Expert initialization function                                   |
//+------------------------------------------------------------------+
int OnInit()
  {
   // Initialize moving averages
   iMA(NULL, 0, fastPeriod, 0, MODE_SMA, PRICE_CLOSE, 0);
   iMA(NULL, 0, slowPeriod, 0, MODE_SMA, PRICE_CLOSE, 0);
   
   return(INIT_SUCCEEDED);
  }
//+------------------------------------------------------------------+
//| Expert tick function                                             |
//+------------------------------------------------------------------+
void OnTick()
  {
   Print("Fast MA: ", iMA(NULL, 0, fastPeriod, 0, MODE_SMA, PRICE_CLOSE, 0));
   Print("Slow MA: ", iMA(NULL, 0, slowPeriod, 0, MODE_SMA, PRICE_CLOSE, 0));
   // Check for moving average crossover
   CheckMACross();
   
   // Execute trading logic
   ExecuteTradingLogic();
  }
//+------------------------------------------------------------------+
//| Function to check moving average crossover                      |
//+------------------------------------------------------------------+
void CheckMACross()
  {
   double fastMA = iMA(NULL, 0, fastPeriod, 0, MODE_SMA, PRICE_CLOSE, 0);
   double slowMA = iMA(NULL, 0, slowPeriod, 0, MODE_SMA, PRICE_CLOSE, 0);
   
   // Determine the crossover signal
   if (fastMA > slowMA)
      maCrossSignal = 1;  // Buy signal
   else if (fastMA < slowMA)
      maCrossSignal = -1; // Sell signal
   else
      maCrossSignal = 0;  // No signal
  }
//+------------------------------------------------------------------+
//| Function to execute trading logic                                |
//+------------------------------------------------------------------+
void ExecuteTradingLogic()
  {
   // Open a buy trade if there's a buy signal
   if (maCrossSignal == 1 && !OrderSend(Symbol(), OP_BUY, lotSize, Ask, 3, 0, 0, "Buy Order", 0, 0, Green))
      Print("Error opening buy order: ", GetLastError());
   
   // Open a sell trade if there's a sell signal
   if (maCrossSignal == -1 && !OrderSend(Symbol(), OP_SELL, lotSize, Bid, 3, 0, 0, "Sell Order", 0, 0, Red))
      Print("Error opening sell order: ", GetLastError());
  }
