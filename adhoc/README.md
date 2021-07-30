Have the VMs running  
```vagrant up```

Test out the inventory file:  
```ansible multi -i inventory -a "hostname"```  

Check disk space of all hosts in Inventory  
```ansible multi -i inventory -a "df -h"```  

Check disk space of single specific host in Inventory  
```ansible -i inventory db -a "df -h```