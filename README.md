# vagrant-dev-examples

Project examples using Ansible Vagrant development environment roles.

Each Ansible role used is continuously integrated and tested using [Goss][goss] and Docker VMs to validate support for
Ubuntu 14.04, Ubuntu 16.04, and CentOS 7. For more information, see the roles projects linked below.

## Supported Languages

Officially supported are the six most popular programming languages at the moment:

 - [Go](./go) ([role][vagrant-go-dev])
 - [Java/Scala/JVM](./java) ([role][vagrant-java-dev])
 - [Node.js](./node) ([role][vagrant-node-dev])
 - [Python](./python) ([role][vagrant-python-dev])
 - [Ruby](./ruby) ([role][vagrant-ruby-dev])
 - [Rust](./rust) ([role][vagrant-rust-dev])

For setups like, e.g. JRuby, these roles can be stacked to provide a combined development environment.

Another "mixin" role that should prove to be useful can be found in the [Docker](./docker) ([role][vagrant-docker])
project. Again, simply mix and match roles applicable to your development needs.

If you would like to add other languages, I'm happy to work with you to build the Ansible roles and tests. Please open
an issue on this project and we will coordinate.

## Supported Operating Systems

As mentioned, Ubuntu 14.04, 16.04, and CentOS 7 are officially supported by these roles, so choose the Vagrant box
that is the most similar to your deployment environment.

## Getting Started

The simplest way to get started is to simply bring down all the files in a language directory into your local project.
Each directory shares the same core files, which are explained presently:

 - `.gitignore`: Ignore `.ansible` and `.vagrant`.
 - `ansible.cfg`: Specify Ansible roles path to `./roles` and `.ansible/galaxy-roles` and add some SSH hacks.
 - `requirements.yml`: Ansible Galaxy requirements file, these Galaxy roles will be downloaded before provisioning.
 - `vagrant.yml`: The Ansible playbook; largely just calls the role defined in `requirements.yml`.
 - `Vagrantfile`: A flexible Vagrantfile configured for the project.

Please feel free to dig through these files and ask questions if anything is unclear.

Once all has been brought down and configured, `vagrant up` will yield a VM with batteries included for your given
development language(s).

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

Go is probably the most distinct setup, requiring one more line to specify the Go package URL.

## License

Licensed at your discretion under either:

 - MIT (`./LICENSE-MIT`)
 - Apache License, Version 2.0 (`./LICENSE-APACHE`)

---

 [vagrant-go-dev]: https://github.com/naftulikay/ansible-role-vagrant-go-dev
 [vagrant-java-dev]: https://github.com/naftulikay/ansible-role-vagrant-java-dev
 [vagrant-node-dev]: https://github.com/naftulikay/ansible-role-vagrant-node-dev
 [vagrant-python-dev]: https://github.com/naftulikay/ansible-role-vagrant-python-dev
 [vagrant-ruby-dev]: https://github.com/naftulikay/ansible-role-vagrant-ruby-dev
 [vagrant-rust-dev]: https://github.com/naftulikay/ansible-role-vagrant-rust-dev
 [vagrant-docker]: https://github.com/naftulikay/ansible-role-vagrant-docker
 [goss]: https://github.com/aelsabbahy/goss
