### Related Refactoring Techniques
|[Universal](README.md)|[C#](CS.md)|
|---|---|

### OOP
+ Use a **serialized public property** to cut down a serialized private field
```cs
// 👎 non-compliant
[SerializeField] private int _level;
public int Level => _level;

// 👍 preference
[field: SerializeField] public int Level {get; private set;}

// 👍 preference: use UsedImplicitly attribute if only assign in Inspector
[field: SerializeField] public int Level {get; [UsedImplicitly] private set;}
[field: SerializeField] [UsedImplicitly] public int Level {get; private set;}
```

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

### Function
+ Pass individual vector components without creating new vector (Unity API usually has overloading method for this, otherwise, create extension method)
```cs
// 👎 non-compliant
_ballRigidbody.AddForce(shotPoint.transform.TransformDirection(new Vector3(0f, 0f, _powerToRoll)));

// 👍 preference
_ballRigidbody.AddForce(shotPoint.transform.TransformDirection(0f, 0f, _powerToRoll));
```

### Animation
+ Use _**hash id**_ to change animator state
> Reason: do not need to validate string each time -> improve performance
```cs
// 👎 non-compliant
void Update(){
  if(attackKey.IsUp()) anim.SetTrigger("Attack");
}

// 👍 performance
private readonly int ATTACK_HASH = Animator.StringToHash("Attack");

void Update(){
  if(attackKey.IsUp()) anim.SetTrigger(ATTACK_HASH);
}
```

### 3rd-Party Asset
+ Wrap asset API usage in its **conditional compiling symbol (directive)** to avoid error on its absence.
> Use [CCU](https://github.com/Unity-Technologies/ConditionalCompilationUtility) to detect and add asset symbol.

### Others
+ ~~```GetComponent```~~ => **```TryGetComponent```** when need to get and use a component:
```cs
// 👎 non-compliant
bulletBody = bullet.GetComponent<Rigidbody>();
if(bulletBody is not null) 
  bulletBody.velocity = transform.forward * speed;

// 👍 preference
if(bullet.TryGetComponent(out Rigidbody bulletBody)
  bulletBody.velocity = transform.forward * speed;
```
