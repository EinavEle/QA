Create a coupon program that has `Coupon`, `User`, and `Store`.
### The `Store`:
- Can assign `Coupon` to `User`.
- Can let a `User` use a `Coupon` if it is valid.

### The `Coupon`:
- Has an id.
- Has an expiry date.
- Has value.
 
### The `User`:
- Has a name.
- Has a list of `Coupon`s

Create the following methods to use coupons:
- by id
- by the highest value from a user's list
- by the closest expiry date from a user's list
- use a randomly selected coupon from a user's list