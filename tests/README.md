# Ansible Role tests

To run the test playbook(s) in this directory:

  1. Install and start Docker.
  1. Make the test shim executable:
     * `chmod +x tests/test.sh`
  1. Run (from the role root directory)
     * `distro=[distro] playbook=[playbook] ./tests/test.sh`

If you don't want the container deleted automatically after running the test playbook, add the following environment variables:

* `cleanup=false`
* `container_id=$(date +%s)`

Credit to [Jeff Geerling](https://www.jeffgeerling.com/)
