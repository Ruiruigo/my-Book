# threading

---

## 添加线程

- **获取已激活线程数**

```
threading.active_count()
```

- **查看所有线程信息**

```
threading.enumerate()
```

- **查看现在正在运行的线程**

```
threading.current_thread()
```

### 添加线程

- **格式**

```python
threading.Thread(group=None, target=None, name=None, args=(), kwargs={}, *, daemon=None)
group 		#应该为 None；为了日后扩展 ThreadGroup 类实现而保留。
target 		#是用于 run() 方法调用的可调用对象。默认是 None，表示不需要调用任何方法。
name 			#是线程名称。默认情况下，由 "Thread-N" 格式构成一个唯一的名称，其中 N 是小的十进制数。
args 			#是用于调用目标函数的参数元组。默认是 ()。
kwargs 		#是用于调用目标函数的关键字参数字典。默认是 {}。
```

