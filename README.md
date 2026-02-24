# chainOfResponsibilityPattern
**Seatwork: BPI ATM System Chain of Responsibility Pattern**

An ATM system for BPI (Bank of the Philippine Islands) needs to efficiently process and dispense cash requests. The machine must dispense cash in specific bill denominations: 1000, 500, 200, 100, 50, and 20 pesos. 

Currently, handling cash dispensing with complex conditional statements (`if-else` or `switch`) for every possible denomination and remainder combination is rigid and difficult to maintain. Adding a new denomination or removing an old one would require modifying the core dispensing logic, violating the Open/Closed Principle.

Implement the Chain of Responsibility Pattern to manage the dispensing of cash requests flexibly and efficiently:

1. **Implement DispenseChain Interface:** Define an interface `DispenseChain` with methods `setNextChain(DispenseChain nextChain)` to link the handlers, and `dispense(Currency currency)` to process the request.
2. **Create a Currency Wrapper:** Define a `Currency` class that encapsulates the integer `amount` to be dispensed.
3. **Define Concrete Dispensers (Handlers):** Create separate classes for each denomination that implement the `DispenseChain` interface: `Peso1000Dispenser`, `Peso500Dispenser`, `Peso200Dispenser`, `Peso100Dispenser`, `Peso50Dispenser`, and `Peso20Dispenser`. 
4. **Implement Handler Behaviors:** Each concrete dispenser checks if the requested amount is greater than or equal to its base denomination. If so, it calculates how many bills to dispense and passes the remainder to the next chain. If not, it simply passes the entire request to the next chain.
5. **Update ATMDispenseChain Class:** * Initialize the chain of responsibility in the constructor.
    * Link the sequence of handlers from highest denomination (1000) to lowest (20).
    * Delegate the initial `dispense()` request to the first handler in the chain.

### Elements of the Pattern

* **Handler:** The concrete classes (`Peso1000Dispenser`, `Peso500Dispenser`, etc.) responsible for dispensing a specific denomination.
* **Chain:** Represented by the `ATMDispenseChain` class. It sets up the sequence of handlers and links them together.
* **Request:** The `dispense()` method call made with a specific `Currency` amount.
* **Client:** The main `BPI_Atm` class that initiates the chain and sends the initial cash request.

### Composition of Dispense Elements

* **nextChain:** DispenseChain (Reference to the next handler)
* **amount:** int (Inside the `Currency` class)

### Methods

* **setNextChain(DispenseChain nextChain):** void *(Links the current handler to the next one)*
* **dispense(Currency cur):** void *(Processes the amount or passes it down the chain)*
* **getAmount():** int *(Retrieves the current value from the Currency object)*

> **Note:** The main program (`BPI_Atm`) should validate that the requested amount is in multiples of 10s before passing the request to the chain, as 20 is the lowest available denomination.

See the `BPI_Atm.java` main class to test the ATM dispenser and its chain execution.
