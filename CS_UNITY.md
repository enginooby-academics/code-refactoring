### Declaration, Initialization & Assignment
+ Refer directly to specific component when _**Instantiate**_ new GameObject
```cs
// 👎 non-compliant
GameObject bullet = Instantiate(bulletPrefab, transform.position, transform.rotation);
bulletBody = bullet.GetComponent<Rigidbody>();
bulletBody.velocity = transform.forward * speed;

// 👍 preference
Rigidbody bulletBody = Instantiate(bulletPrefab, transform.position, transform.rotation);
bulletBody.velocity = transform.forward * speed;
```
