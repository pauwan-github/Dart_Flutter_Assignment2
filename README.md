void main() {
  // Sample list of item prices
  List<double> itemPrices = [5.99, 12.50, 3.75, 25.00, 8.99];

  // Filter items with an anonymous function
  List<double> filteredItems = itemPrices.where((price) => price >= 10).toList();
  
  // Calculate total price with optional tax
  double totalPrice = calculateTotal(filteredItems, tax: 0.07);
  
  // Apply a discount of 10% using a higher-order function
  double discountedPrice = applyDiscount(filteredItems, (price) => price * 0.90);
  
  // Calculate final price after discount and tax
  double finalPrice = calculateTotal(filteredItems, tax: 0.07, discount: discountedPrice);
  
  // Apply a special factorial discount
  double factorialDiscount = calculateFactorialDiscount(filteredItems.length);
  double finalPriceWithFactorialDiscount = finalPrice * (1 - factorialDiscount / 100);

  print("Total Price: \$${totalPrice.toStringAsFixed(2)}");
  print("Discounted Price: \$${discountedPrice.toStringAsFixed(2)}");
  print("Final Price after Tax and Special Discount: \$${finalPriceWithFactorialDiscount.toStringAsFixed(2)}");
}

// Function to calculate total price with optional tax
double calculateTotal(List<double> prices, {double tax = 0.0, double discount = 0.0}) {
  double total = prices.fold(0, (sum, price) => sum + price);
  total -= discount; // Subtract any discount
  total += total * tax; // Add tax
  return total;
}

// Higher-order function to apply a discount
double applyDiscount(List<double> prices, double Function(double) discountFunction) {
  return prices.map(discountFunction).reduce((a, b) => a + b);
}

// Recursive function to calculate factorial discount
double calculateFactorialDiscount(int n) {
  if (n <= 1) return 1; // Base case
  return n * calculateFactorialDiscount(n - 1); // Recursive call
}
