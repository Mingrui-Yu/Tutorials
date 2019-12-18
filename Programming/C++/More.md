# More tricks

## 拼接string

eg:
```
#include <string>

string path = "./data/"+to_string(i+1)+".png";
```

## 计时
使用std::chrono，不要用ctime：
```
#include <chrono>

chrono::steady_clock::time_point t1 = chrono::steady_clock::now();

chrono::steady_clock::time_point t2 = chrono::steady_clock::now();
chrono::duration<double> time_used = chrono::duration_cast <chrono::duration<double>> (t2 - t1);
cout << time_used.count() << "second"; 
```

## 智能指针shared_ptr
```
#include <memory>
```
