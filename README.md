# Buy Fighter Supply Co.

Buy Fighter Supply Co. is a Star Wars-inspired online storefront for browsing fictional spacecraft. Users can view a ship catalog, open individual product pages, add available ships to a cart called the Hangar, remove ships from the cart, and see certain iconic ships marked as sold out.

This project was built for a cloud computing course using OpenClaw on an AWS EC2 instance.

## Project Features

- Homepage for Buy Fighter Supply Co.
- Catalog page with multiple spacecraft listings
- Individual product detail pages
- In-memory shopping cart / Hangar
- Add-to-cart functionality
- Remove-from-cart functionality
- Sold-out logic for unavailable ships
- Millennium Falcon marked as sold out
- Product images hosted in Amazon S3
- Site previewed publicly using Cloudflared

## Tech Stack

- Node.js
- Express.js
- EJS templates
- HTML
- CSS
- JavaScript
- AWS EC2
- Amazon S3
- Cloudflared for public preview access

## AWS Services Used

### EC2

The web application is hosted and run on an AWS EC2 instance. The EC2 instance runs the Node.js Express server and serves the EJS-based storefront.

### S3

Amazon S3 is used to store and serve the ship images used throughout the catalog and product detail pages. Instead of keeping all product images directly on the EC2 instance, the app references image URLs from an S3 bucket.

This makes S3 a meaningful part of the application architecture because it separates static media storage from the web server.

## Application Structure

```text
star-wars-store/
├── app.js
├── package.json
├── README.md
├── data/
│   └── products.js
├── public/
│   └── css/
│       └── style.css
└── views/
    ├── index.ejs
    ├── catalog.ejs
    ├── product.ejs
    ├── cart.ejs
    └── partials/
        ├── header.ejs
        └── footer.ejs
```

## Product Data

The ship catalog is stored in: data/products.js

Each ship has fields such as:

- id
- name
- price
- desc
- img
- soldOut

The img field points to the S3-hosted image URL for each ship.

## Cart Behavior

The cart is stored in memory using a simple JavaScript array inside app.js.

Users can:

- Add available ships to the cart
- View the cart on the Hangar page
- Remove ships from the cart
- See the cart total update

Because the cart is stored in memory, it resets when the Node.js server restarts. This was intentional to keep the project beginner-friendly and focused on the required cloud concepts.

## Sold-Out Behavior

Ships with: soldOut: true

are shown with a sold-out badge.

Sold-out ships cannot be added to the cart from the product page. The backend route also checks soldOut before adding an item to the cart.

The Millennium Falcon is currently marked as sold out as a fun themed feature.

## Security Notes

This project was built in a restricted AWS Learner Lab environment.

The project uses the preconfigured AWS lab permissions instead of creating custom IAM users, roles, or policies. The EC2 instance uses the lab-provided role and instance profile.

No custom IAM roles, users, or policies were created for this project.

The S3 bucket is used only for public product images, not private or sensitive data. Public read access is used so the web app can display product images in the browser.

## OpenClaw Usage

OpenClaw was used as a meaningful development tool throughout the project. It helped with:

- Scaffolding the Express/EJS app
- Creating starter routes and views
- Generating product data
- Improving the catalog and product pages
- Adding sold-out logic
- Adding cart remove functionality
- Troubleshooting syntax and layout issues
- Planning the AWS S3 integration

The code was reviewed, edited, and tested manually on the EC2 instance.

## Current Limitations
- No real payment processing
- No user accounts or authentication
- Cart data is stored in memory and resets on restart
- Product data is stored in a local JavaScript file instead of a database
- Cloudflared public URLs are temporary

These limitations were intentional to keep the first version simple and focused on EC2, S3, and core application functionality.

## Future Improvements

If I had more time, I would consider adding:

- DynamoDB for persistent product or cart data
- CloudWatch for logs and monitoring
- Product filtering or search
- Themed currency options
- More ship categories
- Improved homepage artwork and sci-fi line-art styling
- A more advanced cart with quantities
- Admin-style product editing

## Architecture Summary

Buy Fighter Supply Co. uses EC2 as the compute layer and S3 as the storage layer for static product images.

The Express app runs on EC2 and renders pages with EJS templates. Product metadata is stored locally in data/products.js, while product images are loaded from Amazon S3. Users access the app through a temporary Cloudflared public URL during testing and demo.
