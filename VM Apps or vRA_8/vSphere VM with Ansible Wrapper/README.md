# Cloud VM on vSphere with a wrapper for calling Ansible playbooks with parameters

Extending the built-in ability to call Anbsible playbooks using the wrapper.yml playbook wrapper.
In the obligatory wrapper_playbooks variable, playbooks are passed for execution. The optional variable wrapper_tags accepts tags. The optional wrapper_limit variable adds hosts to the playcube call, and when specified * executes the playbook on the entire inventory.