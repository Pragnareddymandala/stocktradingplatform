import java.util.HashMap;
import java.util.Map;
import java.util.Random;
import java.util.Scanner;

class Stock {
    String symbol;
    double price;

    Stock(String symbol, double price) {
        this.symbol = symbol;
        this.price = price;
    }

    void updatePrice() {
        // Random price fluctuation
        Random random = new Random();
        double change = (random.nextDouble() - 0.5) * 10;  // -5 to +5 change
        price += change;
        if (price < 1) price = 1;  // Avoid negative or zero prices
    }
}
class Portfolio {
    Map<String, Integer> stocks = new HashMap<>();
    double balance;

    Portfolio(double initialBalance) {
        this.balance = initialBalance;
    }

    void buyStock(Stock stock, int quantity) {
        double cost = stock.price * quantity;
        if (balance >= cost) {
            balance -= cost;
            stocks.put(stock.symbol, stocks.getOrDefault(stock.symbol, 0) + quantity);
            System.out.println("Bought " + quantity + " shares of " + stock.symbol + " at $" + stock.price + " each.");
        } else {
            System.out.println("Insufficient balance to buy " + quantity + " shares of " + stock.symbol);
        }
    }

    void sellStock(Stock stock, int 
quantity) {
        int ownedQuantity = stocks.getOrDefault(stock.symbol, 0);
        if (ownedQuantity >= quantity) {
            double revenue = stock.price * quantity;
            balance += revenue;
            stocks.put(stock.symbol, ownedQuantity - quantity);
            System.out.println("Sold " + quantity + " shares of " + stock.symbol + " at $" + stock.price + " each.");
        } else {
            System.out.println("You do not own enough shares to sell " + quantity + " of " + stock.symbol);
        }
    }
void displayPortfolio(Map<String, Stock> market) {
        System.out.println("Portfolio:");
        for (Map.Entry<String, Integer> entry : stocks.entrySet()) {
            String symbol = entry.getKey();
            int quantity = entry.getValue();
            double currentPrice = market.get(symbol).price;
            System.out.println(symbol + ": " + quantity + " shares, Current Price: $" + currentPrice + ", Total Value: $" + (currentPrice * quantity));
        }
        System.out.println("Balance: $" + balance);
    }
}

public class StockTradingPlatform {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        // Initialize market data
        Map<String, Stock> market = new HashMap<>();
        market.put("AAPL", new Stock("AAPL", 150));
        market.put("GOOGL", new Stock("GOOGL", 2800));
        market.put("TSLA", new Stock("TSLA", 700));

        // Initialize user's portfolio
        Portfolio portfolio = new Portfolio(10000);  // Starting with $10,000

        while (true) {
            System.out.println("\n--- Stock Trading Platform ---");
            System.out.println("1. View Market Data");
            System.out.println("2. Buy Stock");
            System.out.println("3. Sell Stock");
            System.out.println("4. View Portfolio");
            System.out.println("5. Exit");
            System.out.print("Choose an option: ");
int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.println("Market Data:");
                    for (Stock stock : market.values()) {
                        stock.updatePrice();
                        System.out.println(stock.symbol + ": $" + stock.price);
                    }
                    break;
                case 2:
                    System.out.print("Enter stock symbol to buy: ");
                    String buySymbol = scanner.next().toUpperCase();
                    if (market.containsKey(buySymbol)) {
                        System.out.print("Enter quantity: ");
                        int quantity = scanner.nextInt();
                        portfolio.buyStock(market.get(buySymbol), quantity);
                    } else {
                        System.out.println("Invalid stock symbol.");
                    }
                    break;
                case 3:
                    System.out.print("Enter stock symbol to sell: ");
                    String sellSymbol = scanner.next().toUpperCase();
                    if (market.containsKey(sellSymbol)) {
                        System.out.print("Enter quantity: ");
                        int quantity = scanner.nextInt();
                        portfolio.sellStock(market.get(sellSymbol), quantity);
                    } else {
                        System.out.println("Invalid stock symbol.");
                    }
                    break;
                case 4:
                    portfolio.displayPortfolio(market);
                    break;
                case 5:
                    System.out.println("Exiting platform.");
                    System.exit(0);
                    break;
                default:
                    System.out.println("Invalid choice.");
            }
        }
    }
}


# stocktradingplatform
codealpha
