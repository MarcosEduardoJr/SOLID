# SOLID


##  S — Single Responsiblity Principle (Princípio da responsabilidade única)


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
##  L — Liskov Substitution Principle (Princípio da substituição de Liskov)
##  I — Interface Segregation Principle (Princípio da Segregação da Interface)
##  D — Dependency Inversion Principle (Princípio da inversão da dependência)
