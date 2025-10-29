Importing Packages

import java.util.*;

This imports Java utility classes — Map, HashMap, Timer, TimerTask, Random, and Scanner — needed for storing rates, updating them, and handling user input.


---

2. Setting Up Exchange Rates

static Map<String, Double> rates = new HashMap<>();

A HashMap stores currency codes and their exchange rates relative to USD.

rates.put("USD", 1.0);
rates.put("EUR", 0.93);
rates.put("INR", 84.12);
rates.put("JPY", 149.23);

These are the initial (base) exchange rates.


---

3. Simulating Live Updates

new Timer(true).scheduleAtFixedRate(new TimerTask() {
    public void run() { updateRates(); }
}, 0, 5000);

This creates a background timer that calls the updateRates() method every 5 seconds.
It simulates live rate changes just like in real currency apps.


---

4. Updating Rates Randomly

static void updateRates() {
    for (String c : rates.keySet()) {
        if (c.equals("USD")) continue;
        rates.put(c, rates.get(c) * (1 + (rand.nextDouble() - 0.5) / 50));
    }
    System.out.println("Rates updated!");
}

Every few seconds, this method slightly increases or decreases each rate by up to ±1%.
This gives the effect of continuously changing (live) exchange rates.


---

5. Taking User Input

Scanner sc = new Scanner(System.in);
System.out.print("From: "); String from = sc.next().toUpperCase();
System.out.print("To: "); String to = sc.next().toUpperCase();
System.out.print("Amount: "); double amt = sc.nextDouble();

The program asks the user for:

Source currency (e.g., USD)

Target currency (e.g., INR)

Amount to convert



---

6. Performing Conversion

double result = amt / rates.get(from) * rates.get(to);
System.out.printf("%.2f %s = %.2f %s%n", amt, from, result, to);

The formula:

converted_amount = (amount / rate_of_source) × rate_of_target

This converts the value based on the latest exchange rates.
