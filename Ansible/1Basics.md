# YAML Basics
http://docs.ansible.com/ansible/latest/YAMLSyntax.html

### Key Value 
Fruit: Apple
Vegetable: Carrot
Liquid: Water
Meet: Chicken

#### Dictionary vs List:
* List: is an Ordered collection
* Dictionary: is an Unordered collection (Order of the property items doesn't matter)
    
### Array/List
Sequences use a dash followed by a space, and it should have equial num of spaces for each values
```
Frouits:
-    Orange
-    Appple
-    Banana

Vegetables:
-    Carrot
-    Cauliflower
-    Tomato
```


### Dictionary/Map
```
Banana:
    Calories: 105
    Fat: 0.4 g
    Carbs: 16 g
```

##### You can have complex type say: Key Value of List containing dictionary
```
Frouits:
    -    Banana:
            Calories: 105
            Fat: 0.4 g
            Carbs: 16 g
    -    Grape:
            Calories: 62
            Fat: 0.3 g
            Carbs: 16 g    
```

            

# Ansible

### [Ansible Inventory](http://docs.ansible.com/ansible/latest/intro_inventory.html) 
Ansible Inventory stores information about list of servers it is connecting to. By default this file is located at /etc/ansible/hosts. To use a different inventory file '-i <path>' option on the command line.
```
$ cat /etc/ansible/hosts

mail.example.com

[webservers]
foo.example.com
bar.example.com

[dbservers]
one.example.com
two.example.com
three.example.com
```


### [Playbook:](http://docs.ansible.com/ansible/latest/playbooks.html)  
Playbook is a list of dictionaries (of Play) (so it is an UnOrdered collection)

##### [Executing A Playbook](http://docs.ansible.com/ansible/latest/playbooks_intro.html#executing-a-playbook)
```
ansible-playbook playbook.yml -f 10
```

### Task: 
Task is a list (so it is an Ordered collection)


### [Loop](http://docs.ansible.com/ansible/latest/playbooks_loops.html)
```
- name: add several users
  user:
    name: "{{ item }}"
    state: present
    groups: "wheel"
  with_items:
     - testuser1
     - testuser2
```
     
### INCLUDE
* include
* vars_files   (used for including variable)

