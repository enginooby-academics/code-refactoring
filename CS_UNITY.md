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

+ Declare **```public```** members which don't need to modify in Playmode w/ **```[HideInInspector]```** attribute
> Reason: clean up Inspector


### Animation
+ Use _**hash id**_ to change animator state
> Reason: do not need to validate string each time -> improve performance
```cs
// 👎 non-compliant
void Update(){
  if(attackKey.IsUp()) anim.SetTrigger("Attack");
}

// 👍 performance
private int attackHash = Animator.StringToHash("Attack");
void Update(){
  if(attackKey.IsUp()) anim.SetTrigger(attackHash);
}
```
