
```
node dist/srp.js

```

```bash
|---srp.ts 
|---order
    |---Order.ts
    |---Product.ts   
    |---Jobs
         |---invoice.ts
         |---PaymentProcessor.ts
         |---PricingCalculator.ts
```         
            
- `order/Product.ts`
```ts
export class Product {

    constructor(id: string, name: string, price: number) {
        this.id = id;
        this.name = name;
        this.price = price;
    }

    id : string;
    name : string;
    price : number;
}
```
- `order/Order.ts`
```ts
import {Product} from "./Product";
export class Order {
    product: Product [] = []

    addProduct(product: Product) {
        this.product.push(product)
    }

    getProduct() {
        return this.product
    }
}
```

- `order/Jobs/invoice.ts`

```ts
import {Product} from "../Product";


export class Invoice {

    generateInvoice(product: Product[] , amount: number) {
        console.log(`
        Invoice Date : ${new Date().toLocaleString()}
        _____________________________
        
        Product Name\t\t\tPrice
        `);

        product.forEach((product:Product)=> {
            console.log(`${product.name}\t\t\t${product.price}`)
        });

        console.log(`_____________________________`);
        console.log(`Total Price : ${amount}`)
    }
}
```

- `order/Jobs/PaymentProcessor.ts`

```ts
import {Order} from "../Order";

export class PaymentProcessor {
    processPayment(order: Order) {
        console.log(`Processing payment...`)
        console.log(`Payment processed successfully.`)
        console.log(`Added to accounting system!`)
        console.log(`Email sent to customer!`)
    }
}
```

- `order/Jobs/PricingCalculator.ts`

```ts
import {Product} from "../Product";


export class PricingCalculator {
    calculatePricing(products: Product[]): number {
        return products.reduce((acc, product) => acc + product.price, 0);
    }
}
```

- `srp.ts`

```ts
import {Product, Order, PricingCalculator, Invoice ,PaymentProcessor} from "./order";


const product1 = new Product("1","Laptop", 200000);
const product2 = new Product("2","Phone", 60000);
const product3 = new Product("3", "Car", 8000000);

const order = new Order();



order.addProduct(product1);
order.addProduct(product2);
order.addProduct(product3);


const pricingCalculator = new PricingCalculator();
const total = pricingCalculator.calculatePricing(order.getProduct());

const invoice = new Invoice();
invoice.generateInvoice(order.getProduct(), total);

const paymentProcessor = new PaymentProcessor();
paymentProcessor.processPayment(order);

```