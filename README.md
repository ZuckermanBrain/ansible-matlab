app-matlab
=========

This role performs an automated install of MATLAB on a Linux host.  It can accomplish this either by copying a folder with the extracted contents of an install ISO to the host, or by mounting an NFS mount containing the extracted contents of an ISO image (see [here](https://www.mathworks.com/matlabcentral/answers/316756-how-can-i-obtain-an-offline-installer-for-matlab-without-using-the-download-only-option-in-the-mat) for instructions about creating an offline installer via _7zip_).  It also creates a service user that owns all of the files installed by MATLAB installer.

For more information about how this role accomplishes a non-interactive installation, see the following links:

 * https://www.mathworks.com/help/install/ug/install-noninteractively-silent-installation.html
 * https://www.mathworks.com/matlabcentral/answers/84-is-there-a-way-to-automate-the-installation-of-matlab
 * https://www.mathworks.com/matlabcentral/answers/332057-how-to-install-matlab-on-linux-environment-with-no-gui

**Note: This role is not currently set up to add standalone licenses, although it can be adapted to do so.**

Role Variables
--------------
`matlab_install` (string) : A relative path to the extracted MATLAB installer ISO within the `files` directory that should be copied to the host if you're not using NFS.  Note that `files` is blacklisted in `.gitignore`.

`matlab_installer_options` (dict): Installation options based off `installer_input.txt` from the install ISO.  These map isomorphically to the options in `installer_input.txt`.  These should be overriden in a group_vars or host_vars file, since the defaults won't work.

`matlab_products` (list) : The Mathworks products that the installer should install.  By default this is empty, since the installer will install.  Only define this list if you want to whitelist the installation of certain toolboxes while blocking the installation of all others.

`matlab_client_network_license` (dict): A dictionary with 3 keys. `fqdn` is the FQDN for the license server, `mac` is the MAC address, and `port` is the port that FLEXnet is listening on.

`matlab_nfs_src` (string): The host:path combination that points to an NFS mount containing an extracted copy of the MATLAB installer ISO.

License
-------

Revised 3-Clause BSD License
