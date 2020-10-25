# Refactoring
## Cashier System

From Chananya's CashAndTrack code: https://github.com/forfeen/CashAndTrack

## In the `CashAndTrack/cashandtrack/Customer.java` class

https://github.com/forfeen/CashAndTrack/blob/master/cashandtrack/Customer.java

consider this code:
```java
    /**
     * To compare the customer
     * @param other
     * @return true if the customer is similarly
     */
    public boolean equalsTo(Customer other) {
        if (other == null) return false;
        for (Customer customer: storeSingleton.getAllCustomer()) {
            if (customer.getCustomerName().toLowerCase().equals(other.getCustomerName().toLowerCase())) {
                if (customer.getMember().equals(other.getMember())) {
                    return true;
                }
            }
        } return false;
    }
```
* Refactoring Signs: 
  - Use many "if" expression.
  - The name of method is ambiguous.
* Refactoring: 
  - Rename method.
    
    In Eclipse or IntelliJ, select the method name and use `Refactor -> Rename` to change it everywhere.
  - use .equalsIgnoreCase() instead of .toLowerCase().equals()
  - Combine if statement in one condition.
  - Remove unnecessary if statement.
```java
    /**
     * To compare the customer
     * @param other
     * @return true if the customer is similarly
     */
    public boolean isCustomerSimilar(Customer other) {
        for (Customer customer: storeSingleton.getAllCustomer()) {
            if (customer.getCustomerName().equalsIgnoreCase(other.getCustomerName() && customer.getMember().equals(other.getMember())) {
                return true;
            }
        } return false;
    }
```
## In the `CashAndTrack/cashandtrack/Menu.java` class

https://github.com/forfeen/CashAndTrack/blob/master/cashandtrack/Menu.java

consider this code:
```java
    /**
     * To compare the menu
     * @param other
     * @return true if the menu is similarly
     */
    public boolean equalsTo(Menu other) {
        if (other == null) return false;
        for (Menu menu : storeSingleton.getAllMenu()) {
            if (menu.getMenuName().toLowerCase().equals(other.getMenuName().toLowerCase())) {
                if (menu.getMenuPrice() == other.getMenuPrice()) {
                    return true;
                }
            }
        }
        return false;
    }
```
* Refactoring Signs: 
  - Use many "if" expression.
  - The name of method is ambiguous.
* Refactoring: 
  - Rename method.
    
    In Eclipse or IntelliJ, select the method name and use `Refactor -> Rename` to change it everywhere.
  - use .equalsIgnoreCase() instead of .toLowerCase().equals()
  - Combine if statement in one condition.
  - Remove unnecessary if statement.

```java
    /**
     * To compare the menu
     * @param other
     * @return true if the menu is similarly
     */
    public boolean isMenuSimilar(Menu other) {
        for (Menu menu : storeSingleton.getAllMenu()) {
            if (menu.getMenuName().equalsIgnoreCase(other.getMenuName()) && menu.getMenuPrice() == other.getMenuPrice()) {
                return true;
            }
        }
        return false;
    }
```


## In the `CashAndTrack/cashandtrack/screen/MenuScreen.java` class

https://github.com/forfeen/CashAndTrack/blob/master/cashandtrack/screen/MenuScreen.java

This class is too large so I change this code:
```java
    private void enterHandler(ActionEvent event)
```
to:
```java
class enterHandler implements EventHandler<ActionEvent> {

        @Override
        public void handle(ActionEvent event) {
```
* Refactoring: Extract method.


## In the `CashAndTrack/cashandtrack/test/CartTest.java` class

https://github.com/forfeen/CashAndTrack/blob/master/cashandtrack/test/CartTest.java

consider this code:
```java
    /** test that remove the order twice.*/
    @Test
    public void testRemoverOrder() throws Exception {
        assertEquals(0, cart.size());
        cart.add(pasta);
        cart.add(pizza);
        assertEquals(2, cart.size());
        cart.remove(pasta);
        cart.remove(pasta);
        assertEquals(1, cart.size());
    }
```
* Refactoring Signs: 
  - The name of the method is not correct. It no vocabulary remover order.
* Refactoring: 
  - Rename method.
```java
    /** test that remove the order twice.*/
    @Test
    public void testRemoveOrderMoreThanOnce() throws Exception {
        assertEquals(0, cart.size());
        cart.add(pasta);
        cart.add(pizza);
        assertEquals(2, cart.size());
        cart.remove(pasta);
        cart.remove(pasta);
        assertEquals(1, cart.size());
    }
```