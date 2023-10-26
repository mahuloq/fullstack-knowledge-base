# you can chain pipes

{{ server.started | date : "fullDate" | uppercase }}

# be careful on the order, as it resolves left to right. It might error if you do it in the wrong order.
