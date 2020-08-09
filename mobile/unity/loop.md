# Loop

#### For loops

#### Arrays

Source : [https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/arrays/multidimensional-arrays](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/arrays/multidimensional-arrays)

**Multi Dimensional Array**

```csharp
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;

public class SafetyPlanScroll : MonoBehaviour
{
    [Header("Safety Form Panels")]
    public GameObject[] SafeForm_4_2_3;
    public GameObject[] SafeForm_4_2_4;
    public GameObject[] SafeForm_4_2_5;
    public GameObject[] SafeForm_4_2_6;
    public GameObject[] SafeForm_4_2_7;
    public GameObject[] SafeForm_4_2_8;


    void Start()
    {
        // Declare the array of two elements.
        basicSafetyArr = new GameObject[6][];

        // Initialize the elements.
        basicSafetyArr[0] = SafeForm_4_2_3;
        basicSafetyArr[1] = SafeForm_4_2_4;
        basicSafetyArr[2] = SafeForm_4_2_5;
        basicSafetyArr[3] = SafeForm_4_2_6;
        basicSafetyArr[4] = SafeForm_4_2_7;
        basicSafetyArr[5] = SafeForm_4_2_8;
    }

    void DisplayData()
    {
        // Display the array elements.
        for (int i = 0; i < basicSafetyArr.Length; i++)
        {
            Debug.Log("Element({0}): " + i);
            for (int j = 0; j < basicSafetyArr[i].Length; j++)
            {
                GameObject game = basicSafetyArr[i][j];

                Debug.Log("Name of elements" + game.name);
                if (game.name == "text-long")
                {
                    string description = game.GetComponent<Text>().text;
                    Debug.Log("description is " + description);
                }

                if (game.name == "InputField")
                {
                    string inputText = game.GetComponentInChildren<Text>().text;
                    Debug.Log("inputText typed is " + inputText);
                }

                if (game.name == "dropdown-button")
                {
                    string optionSelected = game.GetComponentInChildren<Text>().text;
                    Debug.Log("Option selected is " + optionSelected);
                }
            }
        }
    }

}
```

> Jagged Array

Link [https://www.tutorialspoint.com/csharp/csharp\_multi\_dimensional\_arrays.htm](https://www.tutorialspoint.com/csharp/csharp_multi_dimensional_arrays.htm)

#### List

List of same elements, small helper function to help sort unsorted JSON data objects with certain keylist.

```csharp
        Dictionary<DateTime, JSONNode> safeDictionary = new Dictionary<DateTime, JSONNode>();
        JSONArray unsortedseekSafeArray = jsonResponse["scheduled_events"].AsArray;
        List<DateTime> keyList = new List<DateTime>();

        foreach (JSONNode seekSafe in unsortedseekSafeArray)
        {
            DateTime startDate = DateTime.Parse(seekSafe["start_at"]);
            keyList.Add(startDate);
            safeDictionary.Add(startDate, seekSafe);
        }
        keyList.Sort();

        // seekSafe array sorted from oldest to newest seekSafe
        foreach (DateTime date in keyList)
        {
            seekSafeArray.Add(safeDictionary[date]);
        }

        foreach (JSONNode data in seekSafeArray) {
            Debug.Log("Data is ");
            Debug.Log(data["start_at"]);
        }
```

