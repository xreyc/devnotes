#### 1. Sorting
**JavaScript**
```js
const data = [1,2,3,4,5,6,7];
// Ascending
const data.sort((a,b) => a-b);
// Descending
const dart.sort((a,b) => b-a);
```
**Dart**
```dart
List<int> data = [1,2,3,4,5,6,7];
// Ascending
data.sort((a,b) => a.compareTo(b));
// Descending
data.sort((a,b) => b.compareTo(a));
```

#### 2. Filtering
**JavaScript**
```js
const data = [1,2,3,4,5,6,7];
const fdata = data.filter(num => num % 2 == 0);
```
**Dart**
```dart
List<int> data = [1,2,3,4,5,6,7];
List<int> fdata = data.where((int num) => num % 2 == 0).toList();
```

#### 3. Reversing
**JavaScript**
```js
const data = [1,2,3,4,5,6,7];
data.reverse();
```
**Dart**
```dart
List<int> data = [1,2,3,4,5,6,7];
data = data.reversed.toList();
```

#### 4. Map
**JavaScript**
```js
const data = [1,2,3,4,5,6,7];
const fdata = data.map(item => item * item);
```
**Dart**
```dart
List<int> data = [1,2,3,4,5,6,7];
List<int> fdata = data.map((item) => item * item).toList();
```