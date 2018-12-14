​	平时我们在测试一个程序运行时间，一般都会使用DateTime类，在程序运行之前保存一个时间类型，运行之后的时间减去运行之前的时间，就能得到总运行时间。

```c#
DateTime start = DateTime.Now;
//检测运行时间的方法
SomeFunction();
DateTime end =DateTime.Now;
Console.WriteLine("总运行时间:{0}", (end - start).TotalSeconds);
Console.ReadKey();
```

这时之前的方法，其实在.net中提供了一个更专业的类 **Stopwatch** 去处理这个问题。下面看看这个类的详解。

### Stopwatch类

#### 方法

##### public Stopwatch();

```c#
//只有一个无参的构造函数
public Stopwatch();
```

#####  public static long GetTimestamp();

获取运行时长的时间戳

#####  public void Reset();

停止时间间隔测量，并将运行时间重置为零。

#####  public void Restart();

停止时间间隔测量，将运行时间重置为零，然后开始测量运行时间。

#####  public void Start();

开始或继续测量某个时间间隔的运行时间。

#####  public static Stopwatch StartNew();

对新的 System.Diagnostics.Stopwatch 实例进行 **初始化**，将运行时间属性设置为零，然后开始测量运行时间。

#####  public void Stop();

停止测量某个时间间隔的运行时间。

#### 属性

##### public TimeSpan Elapsed { get; }

获取时间间隔，用于表示当前实例测量得出的总运行时间。

#####  public long ElapsedMilliseconds { get; }

表示当前实例测量得出的总毫秒数。

#####  public long ElapsedTicks { get; }

一个只读长整型，表示当前实例测量得出的计时器计时周期的总数。

#####  public bool IsRunning { get; }

如果 System.Diagnostics.Stopwatch 实例当前正在运行，并且在对某个时间间隔的运行时间进行测量，则该值为 true；否则为 false。

下面看一个简单的案例。

```c#
static void Main(string[] args)
{
    Stopwatch stopWatch = new Stopwatch();
    stopWatch.Start();
    Thread.Sleep(10000);
    stopWatch.Stop();
    //获取程序的总运行时间，这时一个时间间隔
    TimeSpan ts = stopWatch.Elapsed;
    string elapsedTime = String.Format("{0:00}:{1:00}:{2:00}.{3:00}",
        ts.Hours, ts.Minutes, ts.Seconds,
        ts.Milliseconds / 10);
    Console.WriteLine("RunTime " + elapsedTime);
    Console.ReadKey();
}
```

通过这个类可以更精确地获取到运行时间。