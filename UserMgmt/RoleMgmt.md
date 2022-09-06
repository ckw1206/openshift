# Adding role to users or groups to project
 
### Adding role to User
```
oc adm policy add-role-to-user <role> <user> -n <project>
```

### Removing role from User
```
oc adm policy remove-role-from-user <role> <user> -n <project>
```

### Adding role to Group
```
oc adm policy add-role-to-group <role> <group> -n <project>
```

### Removing role from Group
```
oc adm policy remove-role-from-group <role> <group> -n <project>
```

---

# Manage cluster-wide role

### Adding cluster-wide role to User
```
oc adm policy add-cluster-role-to-user <role> <user>
```

### Removing cluster-wide role from User
```
oc adm policy remove-cluster-role-from-user <role> <user>
```

### Adding cluster-wide role to Group
```
oc adm policy add-cluster-role-to-group <role> <group>
```

### Removing cluster-wide role from Group
```
oc adm policy remove-cluster-role-from-group <role> <group>
```

