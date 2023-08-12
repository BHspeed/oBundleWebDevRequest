# oBundleWebDevRequest

# My BigCommerce Requested Project

This project is a demonstration of my skills in [specific technologies or platforms]. It showcases [brief overview].

## Bigcommerce Store Preview

- **Preview Code**: PreviewCodeHere
- ------------------------------------------------------------------------------------------------------------------
Here  is the Card.html my addition 

-        <!--Added the primary and secondary image on hover-->
            <div>
                            <a href="{{url}}"
                                   class="card-figure__link"
                                   aria-label="{{> components/products/product-info}}"
                                   data-event-type="product-click"
                                >
                    <div class="card-img-container">
                        {{#if name '===' 'Special Item'}}
                            {{> components/common/responsive-img
                                image=image
                                class="card-image primary-image"
                                fallback_size=theme_settings.productgallery_size
                                lazyload=theme_settings.lazyload_mode
                                default_image=theme_settings.default_image_product
                            }}
                            <img src="https://cdn11.bigcommerce.com/s-bejdogp7fk/images/stencil/1280x1280/products/112/376/Item1__44728.1691789586.jpg?c=1" alt="Secondary Image" class="card-image secondary-image" />
                        {{else}}
                            {{> components/common/responsive-img
                                image=image
                                class="card-image"
                                fallback_size=theme_settings.productgallery_size
                                lazyload=theme_settings.lazyload_mode
                                default_image=theme_settings.default_image_product
                            }}
                        {{/if}}
                    </div>

     -------------------------------------------------------------------------------------------------------------
This is my code from Category.html 

<!-- PROJEST REQUEST, 2 BUTTONS ADD AND DELETE FROM CART. -->
The buttons will only apper for the Special Items Category, Which is what I assumed the directions wanted, it did not specify. 


{{#if category}}
  {{#contains category.name 'Special Items'}}
    <!-- Add All To Cart Button -->
    <button id="addAllToCartButton">Add All To Cart</button>
    <!-- End of Add All To Cart Button -->

    <!-- Initially hidden button -->
    <button id="specialButton" style="display: none;">Remove All Items</button>
  {{/contains}}
{{/if}}


<script>

const storefrontCall = async (endpoint, method, body = null) => {
    const url = `https://obundle-demo-request.mybigcommerce.com/api/storefront${endpoint}`;
    const headers = {
        'Content-Type': 'application/json',
    };

    const config = {
        method,
        headers
    };

    if (body && (method !== 'GET' && method !== 'HEAD')) {
        config.body = JSON.stringify(body);
    }

    try {
        const response = await fetch(url, config);

        if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
        }

        return await response.json();
    } catch (error) {
        console.error(error);
        return null;
    }
};

function createCart(route, cartItems) {
  return fetch(route, {
    method: "POST",
    credentials: "same-origin",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify(cartItems),
  })
  .then(response => response.json())
  .then(result => {
      console.log(result);
      if(result.status && result.status === 422) {
        alert("Failed to add to cart. Please check the request.");
      } else {
        alert('All products added to cart!');
      }
  })
  .catch(error => console.error(error));
};


function checkCartItems() {
  const route = '/api/storefront/carts';  // URL to get the current cart's content

  return fetch(route, {
    method: "GET",
    credentials: "same-origin",
    headers: {
      "Content-Type": "application/json"
    },
  })
  .then(response => response.json())
  .then(carts => {
      // If there's at least one cart and it has items, return true
      const hasPhysicalItems = carts.length > 0 && carts[0].lineItems && carts[0].lineItems.physicalItems && carts[0].lineItems.physicalItems.length > 0;
      const hasDigitalItems = carts.length > 0 && carts[0].lineItems && carts[0].lineItems.digitalItems && carts[0].lineItems.digitalItems.length > 0;
      
      return hasPhysicalItems || hasDigitalItems; // Return true if either physical or digital items are present
  })
  .catch(error => {
      console.error("Error checking cart items:", error);
      return false;
  });
}
function updateButtonDisplay(hasItems) {
    const button = document.getElementById('specialButton');
    if(hasItems) {
        button.style.display = 'block';  // Show the button
    } else {
        button.style.display = 'none';  // Hide the button
    }
}


document.addEventListener('DOMContentLoaded', () => {
    console.log("DOMContentLoaded triggered");  // Ensure this log appears

    // Check cart items once the document has been fully loaded.
    checkCartItems().then(hasItems => {
        updateButtonDisplay(hasItems);
    });

    // Event listener for the add all to cart button
    document.getElementById('addAllToCartButton').addEventListener('click', () => {
        const productIds = [...document.querySelectorAll('[data-entity-id]')].map(element => parseInt(element.getAttribute('data-entity-id')));

        const lineItems = productIds.map(id => ({ productId: id, quantity: 1 }));

        createCart(`/api/storefront/carts`, {
            "lineItems": lineItems
        }).then(() => {
            // Check cart items again after items have been added to the cart.
            checkCartItems().then(hasItems => {
                updateButtonDisplay(hasItems);
            });
        });
    });
});
//Event listener for the delete all from cart button
document.getElementById('specialButton').addEventListener('click', async () => {
    // First, fetch the current cart and its items
    const route = '/api/storefront/carts';

    try {
        const carts = await fetch(route, {
            method: "GET",
            credentials: "same-origin",
            headers: {
                "Content-Type": "application/json"
            }
        }).then(response => response.json());

        if (!carts.length) {
            console.log('No cart found!');
            return;
        }

        const cartId = carts[0].id;
        const items = carts[0].lineItems.physicalItems.concat(carts[0].lineItems.digitalItems); // Get both physical and digital items
        
        // For each item in the cart, send a DELETE request
        for (let item of items) { 
            await fetch(`https://obundle-demo-request.mybigcommerce.com/api/storefront/carts/${cartId}/items/${item.id}`, {
                method: 'DELETE',
                headers: {
                    'Content-Type': 'application/json'
                }
            });
        }

        alert('All items removed from cart!');

        // Re-check the cart items and update button display after deletion
        checkCartItems().then(hasItems => {
            updateButtonDisplay(hasItems);
        });

    } catch (err) {
        console.error('Error removing items from cart:', err);
    }
});


</script>
-----------------------------------------------------------------------------
- **URL**: [Your Bigcommerce Store URL](https://obundle-demo-request.mybigcommerce.com/)

Please note that the preview code may change, so if there are any issues accessing the store, kindly contact me.
