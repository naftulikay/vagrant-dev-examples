# vagrant-dev-examples

Project examples using my Ansible Vagrant development environment roles.

## Getting Started

The simplest way to get started is to simply bring down all the files in a language directory into your local project.
Each directory shares the same core files, which are explained presently:

 - `.gitignore`: Ignore `.ansible` and `.vagrant`.
 - `ansible.cfg`: Specify Ansible roles path to `./roles` and `.ansible/galaxy-roles` and add some SSH hacks.
 - `requirements.yml`: Ansible Galaxy requirements file, these Galaxy roles will be downloaded before provisioning.
 - `vagrant.yml`: The Ansible playbook; largely just calls the role defined in `requirements.yml`.
 - `Vagrantfile`: A flexible Vagrantfile configured for the project.

Please feel free to dig through these files and ask questions if anything is unclear.

## Differences

Differences between different languages are very slight and can be best summed up in this small diff:

```diff
diff --git a/node/requirements.yml b/python/requirements.yml
index 2f07e4a..e7ca4ab 100644
--- a/node/requirements.yml
+++ b/python/requirements.yml
@@ -1,3 +1,3 @@
 ---
-- src: naftulikay.vagrant-node-dev
-  name: vagrant-node-dev
+- src: naftulikay.vagrant-python-dev
+  name: vagrant-python-dev
diff --git a/node/vagrant.yml b/python/vagrant.yml
index e760c5c..3dcc8b1 100644
--- a/node/vagrant.yml
+++ b/python/vagrant.yml
@@ -3,5 +3,5 @@
   hosts: all
   become: true
   roles:
-    - role: vagrant-node-dev
-      node_version: 8.9.4
+    - role: vagrant-python-dev
+      python_version: 2.7.5
```

## License

Licensed at your discretion under either:

 - MIT (`./LICENSE-MIT`)
 - Apache License, Version 2.0 (`./LICENSE-APACHE`)
