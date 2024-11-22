
This Repo will show you how to install the basic monolithic iteration of Grafana k6. I wanted to give my classmates the ability to conduct load tests in the instance they want to test their infrastructure and view their metrics via monitoring tools such as Prometheus.  

Now, Grafana k6 comes in 2 iterations. The monolithic release *"our example today"* and the Kubernetes version. As you will soon see it is rather simple to install the sole tenant version. The Kubernetes version however requires *".make file"* configurations upon each use and subsequent steps to correctly deploy ephemeral batch pods. However what the Kubernetes version lacks in simplicity. It makes up in terms of scalability and the power at which you can run your tests without worry for the underlying hardware. 

If you're brave like me, follow the below link and give the Kubernetes version a try! 
https://grafana.com/blog/2022/06/23/running-distributed-load-tests-on-kubernetes/

---
## Installation and basic deployment

To install the monolithic version of k6 is rather simplistic. 

Windows users open PowerShell to avoid issues and Mac users rejoice and open your terminals. 

Enter the below command for your machine type:

Windows Savages:
```python
choco install k6
```

Bashful Macs:
```python
brew install k6
```


After instillation confirm the installation went smoothly using `k6 version`.

If everything is hunky dory, deploy a public facing application you had in mind to begin running tests. 

And in a separate for a clean work space run the following command:
```python
$ k6 new
```

This will in turn generate a basic tutorial JavaScript file to run k6 tests on. K6 devises the instructions for the deployments of it's programmatically via JavaScript. Using basic functions You can define the following traits for testing: 

- Amount of virtual users
- Duration of the prescribed user amount
- Failed requests 
- Random pauses in traffic
- etc...

All of these features can be written to throttle up and down during testing. So the world is quite literally your oyster. 

Now if you enter the file I want you to pay attention to one specific thing to get started quickly.
Can you find the field in which you specify the target URL for your test? 

It should look something like this:
```python
export default function() {
  http.get('https://test.k6.io');
  sleep(1);
}
```
It's painfully obvious, but this is where you define your target in order to proceed. Replace this with the external Ip of the application you desire to test. 

Now we can cook. 
Go into your terminal or git bash and execute your script using the following:
```python
$ k6 run script.js
```
And now you should see the decorative output and the resulting information from your first basic test. 

I'd recommend reading the following article for clarification on best practices for writing tests:
https://grafana.com/docs/k6/latest/testing-guides/test-types/

And this article for more details into writing k6 scripts:
https://grafana.com/docs/k6/latest/get-started/running-k6/

Within my attached repo you'll see an example of the 3 varying scripts I've used to test different integrations of my Kubernetes including Istio.  

Please try them out and Send me screenshots of your test results!

