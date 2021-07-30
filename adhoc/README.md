Have the VMs running
```vagrant up```

Test out the inventory file:  
```ansible multi -i inventory -a "hostname"```  

Check disk space of hosts in Inventory  
```ansible multi -i inventory -a "df -h"```