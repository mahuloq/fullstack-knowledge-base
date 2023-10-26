{{ server.instanceType | uppercase }} |
{{ server.started | date }}

# These basic pipes turn the content to all uppercase, or format the date to be more readable.

# You can customize a pipe with parameters by doing

{{ server.started | date : "fullDate" }}

# if the pipe takes multiple parameters you would show them like

{{ server.started | date : "fullDate":'parameter' }}
