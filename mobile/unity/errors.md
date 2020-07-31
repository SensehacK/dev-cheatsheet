# Errors

### Errors

> NullReferenceException: Object reference not set to an instance of an object

> There is no GameObject attached to this GameObject

[Link](https://answers.unity.com/questions/1393443/there-is-no-gameobject-attached-to-this-gameobject.html)

When using INSTANCE variable for singleton property, we need to invoke the awake function unity life cycle to set the variable with this.

Parent\_Class

```csharp
public class SafetyPlanManager : MonoBehaviour
{

 public static SafetyPlanManager _instance = null;

 public static SafetyPlanManager Instance
 {
  get { return _instance; }
 }

 private void Awake()
    {
  Debug.Log("In Awake SafetyPlanManager");
        if (Instance == null)
        {
            _instance = this;
        }
        else if (Instance != this)
        {
            Destroy(this);
        }
    }

 void Start()
 {
  Debug.Log("In Start SafetyPlanManager");
  // Invoking the personalized class.
  SafetyPlanPersonalized.Instance.InitializeUI(true);
 }
}
```

Child\_Class

```csharp
public class SafetyPlanPersonalized : MonoBehaviour
{

 public static SafetyPlanPersonalized _instance = null;

 public static SafetyPlanPersonalized Instance
 {
  get { return _instance; }
 }

 private void Awake()
    {
  Debug.Log("In Awake SafetyPlanPersonalized");
        if (Instance == null)
        {
            _instance = this;
        }
        else if (Instance != this)
        {
            Destroy(this);
        }
    }

 public void InitializeUI(bool isFirstLogin) {}
}
```

// Important Note:

In order the child class to be used with Instance variable, the calling parent class should also set its instance variable to this \(currently instance\)

