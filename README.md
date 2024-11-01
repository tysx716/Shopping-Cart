# Shopping-Cart
//Building a Shopping cart using Javascript. 
// define an array of product objects, each with a name, price, productId, and image
const products = [
  {
    name: "Cherry",
    price: 2.99,
    quantity: 0, // initial quantity in cart is set to zero
    productId: 1,
    image: "./images/cherry.jpg"
  },
  {
    name: "Orange",
    price: 4.99,
    quantity: 0, // initial quantity in cart is set to zero
    productId: 2,
    image: "./images/orange.jpg"
  },
  {
    name: "Strawberry",
    price: 3.99,
    quantity: 0, // initial quantity in cart is set to zero
    productId: 3,
    image: "./images/strawberry.jpg"
  },
]
// Initialize an empty array to hold items added to the shopping cart
let cart = [];
function  getProductbyId(productId, productList) {
   return productList.find((product) => product.productId  === productId);
   
}



function addProductToCart(productId) { 
 let product = getProductbyId(productId, products);

 // If the product is found
  if (product) {
      product.quantity += 1;
  // add to cart only if it's not already present
  if (!getProductbyId(productId, cart)) {
    cart.push(product);
    }
  }
}

function increaseQuantity(productId) {
  let product = getProductbyId(productId, cart)
  if (product) {
    product.quantity += 1;
  }
  const cartItem = cart.find(item => item.productId === productId);
  // if product is found in the cart, increase quantity
  if (cartItem) cartItem.quantity += 1;
}

function decreaseQuantity(productId) {
  let product = getProductbyId(productId, cart);
  const cartItem = cart.find(item => item.productId === productId);
  //if product is found in cart
  if (cartItem) {
    if (cartItem.quantity > 1) {
      cartItem.quantity -= 1;

    if (cartProduct.quantity === 0) {
      removeProductFromCart(productId);
      }
    }
  }
}
/**
 * removedProductFromCart(productId)
 * 
 * This function removes a product from th cart based on the provided productId
 * 
 * Steps:
 * 1.Find the product in the cart with the specified productId.
 * 2.Sets the product's quantity back to zero to reflect its removal. 
 * 3.Removes the product from the cart array by using a method that modifes the array directly
 * 
 * This function helps ensure the cart only contains products with a quantity greater than zero. 
 * @param {number} productId 
 */

function removeProductFromCart(productId) {
  let product = getProductbyId(productId, cart);

  // find the index of the product in the cart

if (product) {
  product.quantity = 0;

  const index = cart.indexOf(product);
  if (index !== -1) {
    cart[index].quantity = 0;
    cart.splice(index, 1);
   } 
  }
}

function cartTotal() {
  // Multiply each product's price by quantity and sum up
  return cart.reduce((total, item) => total + (item.price * item.quantity), 0);
}

function emptyCart () {
  cart.forEach(product => {
    removeProductFromCart(productId);
  });
  //clear the cart array
  cart = [] ;
}

let balance = 0;
let totalPaid = 0;

function pay(amount) {
  totalPaid += amount;
  let remaining = totalPaid - cartTotal();
  if (remaining >= 0) {
    totalPaid = 0;
    emptyCart();
    
  }
  return remaining;
}
module.exports = {
  products,
  cart,
  addProductToCart,
  increaseQuantity,
  decreaseQuantity,
  removeProductFromCart,
  cartTotal,
  pay, 
  emptyCart,
  /* Uncomment the following line if completing the currency converter bonus */
  // currency
}
