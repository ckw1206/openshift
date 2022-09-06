# Manage local role

### Assign local role to User
```
oc adm policy add-role-to-user <role> <user>
```

### Remove local role to User
```
oc adm policy remove-role-from-user <role> <user>
```

### Assign local role to Group
```
oc adm policy add-role-to-group <role> <group>
```

### Remove local role to Group
```
oc adm policy remove-role-from-group <role> <group>
```

---

# Manage cluster-wide role

### Assign cluster-wide role to User
```
oc adm policy add-cluster-role-to-user <role> <user>
```

### Remove cluster-wide role to User
```
oc adm policy remove-cluster-role-from-user <role> <user>
```

### Assign cluster-wide role to Group
```
oc adm policy add-cluster-role-to-group <role> <group>
```

### Remove cluster-wide role to Group
```
oc adm policy remove-cluster-role-from-group <role> <group>
```

