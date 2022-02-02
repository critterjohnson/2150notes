---
slug: "/notes/lists"
date: "2022-02-02"
title: "Lists"
---

# Lists

## C++ Templates

- function templates
- class templates

### Function Templates

- not an actual function, but a pattern

```cpp
template <typename Comparable>
const Comparable& findMax(const vector<Comparable>& a) {
        int maxIndex = 0;
        for(int i = 1; i < a.size(); i++) {
                if (a[maxIndex] < a[i])
                        maxIndex=i;
        }
        return a[maxIndex];
}

int main() {
        vector<int> v1(30);
        cout << findMax(v1) << endl; // this is expanded at compile time
}
```
