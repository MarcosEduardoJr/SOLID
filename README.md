# SOLID


##  S — Single Responsiblity Principle (Princípio da responsabilidade única)

The idea behind the SRP is that every class, module, or function in a program should have one responsibility/purpose in a program. As a commonly used definition, "every class should have only one reason to change".

### Before
```
public class Product {
 private String description;
 private int count;
 private long price;
}

public class order{
private int numberOrder;
private List<Product> products = new ArrayList<>();
}


Some RecyclerAdapter:
@Override public void onBindViewHolder(ViewHolder holder, int position){
  Order order = items.get(position);
  
  holder.numberOrder.setText(order.getNumberOrder().toString());
  
  long total = 0;
  for(Product product : order.getProducts()){
    total += product.getPrice();
  }
 //. . . show the total order to user
}
```

### After
```
public class order{
  private int numberOrder;
  private List<Product> products = new ArrayList<>();

public long getValueTotalOrder(){
  long total = 0;
  for ( Product product : order.getProducts()){
  total += product.getPrice();
  }
  return total;
}
}


@Override public void onBindViewHolder(ViewHolder holder, int position){
  Order order = items.get(position);
  
  holder.numberOrder.setText(order.getNumberOrder().toString());
  
   holder.valueTotalOrder.setText(order.getValueTotalOrder().toString());
}

```


##  O — Open-Closed Principle (Princípio Aberto-Fechado)

The open-closed principle states that software entities should be open for extension, but closed for modification.

This implies that such entities – classes, functions, and so on – should be created in a way that their core functionalities can be extended to other entities without altering the initial entity's source code.

In the example below, the app need now calculate discount of order, but the code have a lot of conditions :

### Before
```
private static int  DISCOUNT_10_PEER_CENT = 1
private static int DISCOUNT_15_PEER_CENT = 2

private int typeDiscount;
public long getValueTotalOrder(){
  long total = 0;
  for ( Product product : order.getProducts()){
  total += product.getPrice();
  }
  long discount = 0;
  if(typeDiscount == DISCOUNT_10_PEER_CENT){
     discount = total * 0.1;
  } else if (typeDiscount == DISCOUNT_15_PEER_CENT){
  discount = total * 0.15;
  }
  total += discount;
  return total;
}

```
### After

To resolve this, we can use INTERFACE : 
```
public interface Discount{
 long calculateDiscount(long value);
}

public class Discount10PeerCent implements Discount{
 public  long calculateDiscount(long value){
  return value * 0.1;
 }
}

public class Discount15PeerCent implements Discount{
 public  long calculateDiscount(long value){
  return value * 0.15;
 }
}

```

##  L — Liskov Substitution Principle (Princípio da substituição de Liskov)

The Liskov substitution principle simply implies that when an instance of a class is passed/extended to another class, the inheriting class should have a use case for all the properties and behavior of the inherited class.

Let's say we have a class called Amphibian for animals that can live on both land and water. This class has two methods to show the features of an amphibian – swim() and walk().
 
```
public class Amphibian {

    public void swim();
    public void walk();

}

public class Frog extends Amphibian {
    public void swim() {
        System.out.println("The frog is swimming");
    }
    
    public void walk() {
        System.out.println("The frog is walking on land");
    }
}

But we cannot extend the Amphibian class to a Dolphin class because dolphins only live in water which implies that the walk() method would be irrelevant to the Dolphin class.

So, when you extend a class, if some of the properties of the initial class are not useful for the new class, the Liskov substitution principle has been violated.

The solution to this is simple: create interfaces that match the needs of the inheriting class.

In summary, if a class inherits another, it should do so in a manner that all the properties of the inherited class would remain relevant to its functionality.

```
 
##  I — Interface Segregation Principle (Princípio da Segregação da Interface)


### Before
```
```
### After
```
```
##  D — Dependency Inversion Principle (Princípio da inversão da dependência)

### Before
```
```
### After
```
```
