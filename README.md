Role Name
=========

A utility role to pull container images from a registry and save the tar files for each image in the list to the designated location as an atomic transaction.
It pulls the image, tars it and then remove the image from the local runtime container cache so as to not cause any out of disk errors 
when several images are synched. It also will retry to pull if the image pull fails for the first time. 

Requirements
------------

Podman is expected to the installed on the target system.

Role Variables
--------------
This role expects the following variables:
images_to_process: List (Dictionary) of images to sync in the format of fully qualified name of image and version (e.g. quay.io/myrepo/myimage:v0.1). It that variable is not set but the optional variable images is set the role will use that value to set this variable.
mirred_content_local_dir: the local directory to mirror the image tar files to. If this is not set and the optional sync_dir variable is set then that value is used to set this variable.
registry_auth_file: The auth file (in docker config json format) needed to authenticate with the registry. If that value is not set then registry_username and registry_password are required.
registry_username: username to use to authenticate against the registry. If the registry_auth_file is not set then this variable and the next are use to create the auth file .
registry_password: password for the user to use to authenticate against the registry.


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: localhost 
      roles:
         - { role: image-sync, registry_username:registry-user, registry_password: mypassword, mirred_content_local_dir: "/data", images: "" }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
