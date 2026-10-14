# Change configuration port speed
```
Router(config)# line console 0
Router(config)# speed 9600
Router# write memory 
```
# Stop being interrupted by logs
```
Router(config)# line console 0
Router(config-line)# logging synchronous
```