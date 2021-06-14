# Konnect Data Plane

Install the [Kong Gateway](https://github.com/kong/kong) and register it with [Konnect](https://konghq.com/kong-konnect/) for use as a data plane.

## Role Variables

- `konnect_username`: Your Konnect username
- `konnect_password`: Your Konnect password

You can provide these by running `ansible-playbook playbook.yml --extra-vars "konnect_username=user@example.com konnect_password=SuperSecureP455W0rD"` for testing, or use [Ansible Vault](https://docs.ansible.com/ansible/latest/user_guide/vault.html) for production.

## Usage

Create a file named `playbook.yml` with the following contents:

```yaml
---
- hosts: all
  roles:
    - role: "mheap.konnect-data-plane"
```

In the same directory, create a folder named `roles` and change directory into it. Next, clone this repo into the `roles` directory.

Execute the playbook by running the following command in the same directory as `playbook.yml`:

```bash
ansible-playbook -i "ip_addr," playbook.yml --extra-vars "konnect_username=user@example.com konnect_password=SuperSecureP455W0rD
```

### Using Vagrant

To test with Vagrant, create a file named `Vagrantfile` with the following contents then run `vagrant up`:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.compatibility_mode = "2.0"
    ansible.extra_vars = {
      konnect_username: "user@example.com",
      konnect_password: "SuperSecureP455W0rD",
    }
  end

end
```

When it finishes building the machine will be registered in Konnect as a data plane.

## License

MIT

## Author Information

Michael Heap <michael.heap@konghq.com>
