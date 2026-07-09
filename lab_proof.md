# LAB PROOF | Day 2 | Data Manipulation + JSON Handling
## John Adams

## Program path:
See `titanic_analysis.ipynb` file

## Output

**Statistical calculations:**
```
Mean:
PassengerId    446.000000
Survived         0.383838
Pclass           2.308642
Age             29.699118
SibSp            0.523008
Parch            0.381594
Fare            32.204208
dtype: float64

Median:
PassengerId    446.0000
Survived         0.0000
Pclass           3.0000
Age             28.0000
SibSp            0.0000
Parch            0.0000
Fare            14.4542
dtype: float64

Standard Deviation:
PassengerId    257.353842
Survived         0.486592
Pclass           0.836071
Age             14.526497
SibSp            1.102743
Parch            0.806057
Fare            49.693429
dtype: float64
```

**Missing value analysis:**
```
==================================================
MISSING VALUES ANALYSIS
==================================================
Column: PassengerId, Missing Values: 0, Percentage: 0.00%
Column: Survived, Missing Values: 0, Percentage: 0.00%
Column: Pclass, Missing Values: 0, Percentage: 0.00%
Column: Name, Missing Values: 0, Percentage: 0.00%
Column: Sex, Missing Values: 0, Percentage: 0.00%
Column: Age, Missing Values: 177, Percentage: 19.87%
Column: SibSp, Missing Values: 0, Percentage: 0.00%
Column: Parch, Missing Values: 0, Percentage: 0.00%
Column: Ticket, Missing Values: 0, Percentage: 0.00%
Column: Fare, Missing Values: 0, Percentage: 0.00%
Column: Cabin, Missing Values: 687, Percentage: 77.10%
Column: Embarked, Missing Values: 2, Percentage: 0.22%
```

**Feature engineering results:**
```
   SibSp  Parch  FamilySize
0      1      0           2
1      1      0           2
2      0      0           1
3      1      0           2
4      0      0           1
5      0      0           1
6      0      0           1
7      3      1           5
8      0      2           3
9      1      0           2
   FamilySize  IsAlone
0           2    False
1           2    False
2           1     True
3           2    False
4           1     True
5           1     True
6           1     True
7           5    False
8           3    False
9           2    False
    Age     AgeGroup
0  22.0  Young Adult
1  38.0        Adult
2  26.0  Young Adult
3  35.0        Adult
4  35.0        Adult
5   NaN      Unknown
6  54.0       Senior
7   2.0        Minor
8  27.0  Young Adult
9  14.0        Minor

==================================================
FEATURE ANALYSIS: SURVIVED vs NOT SURVIVED
==================================================

Family Size by Survival:
              mean  median       std
Survived
0         1.883424     1.0  1.830669
1         1.938596     2.0  1.186076

==================================================
FEATURE DIFFERENTIATION ANALYSIS
==================================================

Family Size:
  Survived mean: 1.94
  Not Survived mean: 1.88
  Difference: 0.06
```

## JSON export validation:
```
# Additional validation: Load and inspect JSON
with open(JSON_FILE, 'r', encoding='utf-8') as f:
    json_data = json.load(f)
 
# Print summary of JSON data and verify content
print("Top-level keys:", list(json_data.keys()))
print("Metadata:", json_data['metadata'])
print("Number of passenger records:", len(json_data['passengers']))
```

```
Dataset Information:
Total passengers: 891
Survival rate: 0.3838383838383838

total_passengers: 891
survived: 342
did_not_survive: 549
average_age: 29.69911764705882
average_fare: 32.204207968574636

Data exported to data/titanic_data.json

Top-level keys: ['metadata', 'passengers']
Metadata: {'dataset_name': 'Titanic Passenger Dataset', 'export_date': '2026-07-09T16:35:08.778947', 'total_passengers': 891, 'survival_rate': 0.3838383838383838}
Number of passenger records: 891
```

## Explanation:

I created three:
- `FamilySize` = adds `SibSp` and `Parch` together and +1 for the passenger
- `IsAlone` = checks if `FamilySize` is equal to 1
- `AgeGroup` = sorts passengers into Minor, Young Adult, Adult, and Senior based on their age

When comparing `FamilySize` between people who survived and people who didn't, the numbers were pretty close (1.94 and 1.88), so on its own this feature doesn't appear to show anything major about who survived. Looking at the others it's interesting that `IsAlone` and `AgeGroup` likely had a bigger impact given children may have been given priority ("women and children first") in boarding life rafts, and if you had a family nearby to help you get to a lifeboat versus being on your own in the chaos.

When using classes for data processing, I learned that putting passenger data into an object, with the `to_dict()` method made it easier to export into the JSON. The object handled its own processing without repetition.