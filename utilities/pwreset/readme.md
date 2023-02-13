### Password Reset Script

The intention here is to be able to reset user passwords on selected servers.

In some cases, we want different passwords for each environment, hence the different environment name and password. If the person will have the same password across all environments, simply set it as such across all the entries in the vault file.

Speaking of the vault file, it should have a list of the environments and then the password is associated with the user for each one.

For example:

    ---
    username: 'username'
    boulder: 'hashed password'
    longmont: 'hashed password'

You can generate the password in any way you wish. There is a password generation script on the servers in /opt/unixsuite/bin/password. It returns five randomly generated of 10 characters each.

You'll need to generate a hash for the vault file. Use the python command as follows:

    'python -c "from passlib.hash import sha512_crypt; import getpass; print sha512_crypt.encrypt(getpass.getpass())"'

You'll also need to modify the pwreset/tasks/main.yaml playbook if you have different environments than I have (very likely :) ).

