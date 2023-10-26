# if you are waiting for some data like below

appStatus = new Promise((resolve, reject) => {
setTimeout(() => {
resolve("stable");
}, 2000);
});

# and are trying to display it like

  <h3>App Status: {{ appStatus}}</h3>

# you will get object Promise or object Object displayed.

  <h3>App Status: {{ appStatus | async }}</h3>

# with async added, it knows to wait for data.
