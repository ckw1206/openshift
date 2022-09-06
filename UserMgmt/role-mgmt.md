# Adding role to users or groups to project
 
### To add role to User
```
oc adm policy add-role-to-user <role> <user> -n <project>
```

### To remove role from User
```
oc adm policy remove-role-from-user <role> <user> -n <project>
```

### To add role to Group
```
oc adm policy add-role-to-group <role> <group> -n <project>
```

### To remove role from Group
```
oc adm policy remove-role-from-group <role> <group> -n <project>
```

---

# Manage cluster-wide role

### To add cluster-wide role to User
```
oc adm policy add-cluster-role-to-user <role> <user>
```

### To remove cluster-wide role from User
```
oc adm policy remove-cluster-role-from-user <role> <user>
```

### To add cluster-wide role to Group
```
oc adm policy add-cluster-role-to-group <role> <group>
```

### To remove cluster-wide role from Group
```
oc adm policy remove-cluster-role-from-group <role> <group>
```

