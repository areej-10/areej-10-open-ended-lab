This README.md is structured to help you document your progress through Lab 14. It follows the exact task list and includes placeholders for all required screenshots to ensure a complete submission.

Lab 14 – Terraform + Ansible: Dynamic Inventory, Roles & Automated Deployment
📋 Project Overview
This project demonstrates a full CI/CD infrastructure-as-code (IaC) workflow. It uses Terraform to provision AWS infrastructure and Ansible to configure software, manage SSL certificates, and deploy Dockerized applications (Gitea). The lab concludes with automating the Ansible execution directly from Terraform and implementing a dynamic inventory using the aws_ec2 plugin.

🛠 Prerequisites
GitHub Codespace (Linux environment)

AWS CLI & Terraform pre-installed

Ansible-core (installed via pipx)

AWS IAM Credentials for me-central-1

🚀 Tasks and Implementation
Task 0 – Lab Setup
Forked and opened the terraform_machine repository in Codespaces.

Verified environment versions and AWS authentication.

Screenshots: task0_codespace_open.png, task0_env_check.png, task0_aws_config.png

Task 1 – SSH Key & Initial Apply
Generated an Ed25519 SSH key pair for instance access.

Configured terraform.tfvars with environment-specific variables.

Provisioned 2 initial EC2 instances.

Screenshots: task1_ssh_keygen_before.png, task1_ssh_keygen.png, task1_ssh_keygen_after.png, task1_terraform_tfvars_created.png, task1_terraform_tfvars.png, task1_terraform_init.png, task1_terraform_apply_2_instances.png, task1_terraform_output_ips.png

Task 2 – Static Ansible Inventory
Installed ansible-core using pipx.

Created a static hosts file and tested connectivity using the ping module.

Screenshots: task2_ansible_install.png, task2_terraform_output_ips.png, task2_hosts_created.png, task2_hosts_initial.png, task2_ansible_ping_initial.png, task2_hosts_with_common_args.png, task2_ansible_ping_success.png

Task 3 – Scale to Three Instances
Modified main.tf to use count = 3.

Updated the hosts file with grouped inventory ([ec2] and [droplet]).

Screenshots: task3_main_tf_count_3.png, task3_terraform_apply_3_instances.png, task3_terraform_output_3_ips.png, task3_hosts_grouped.png, task3_ansible_ec2_ping.png, task3_ansible_single_ip_ping.png, task3_ansible_droplet_ping.png, task3_ansible_all_ping.png

Task 4 – Global Configuration & First Playbook
Created ~/.ansible.cfg to disable host key checking globally.

Wrote my-playbook.yaml to install and start Nginx.

Screenshots: task4_global_ansible_cfg.png, task4_hosts_without_common_args.png, task4_ansible_ping_after_cfg.png, task4_my_playbook_created.png, task4_my_playbook_ec2.png, task4_ansible_play_ec2.png, task4_nginx_browser_ec2.png, task4_my_playbook_droplet.png, task4_ansible_play_droplet.png, task4_nginx_browser_droplet.png

Task 5 – Single Target & HTTPS Prep
Created a project-level ansible.cfg.

Scaled back to 1 instance and added openssl to the playbook.

Screenshots: task5_project_ansible_cfg_created.png, task5_project_ansible_cfg.png, task5_main_tf_count_1.png, task5_terraform_apply_one_instance.png, task5_terraform_output_single_ip.png, task5_hosts_nginx_group.png, task5_my_playbook_nginx_group.png, task5_ansible_play_nginx_group.png, task5_nginx_browser_single.png

Task 6 – Self-Signed SSL Certificates
Used Ansible uri module to fetch EC2 metadata (IMDSv2).

Automated the generation of self-signed certificates with the instance's public IP as the Common Name (CN).

Screenshots: task6_my_playbook_ssl_section.png, task6_ansible_play_ssl.png, task6_ssl_cert_file.png, task6_ssl_key_file.png

Task 7 – PHP Front-End Deployment
Deployed a PHP metadata page using Jinja2 templates for the Nginx configuration.

Verified secure access via HTTPS.

Screenshots: task7_files_templates_created.png, task7_index_php_content.png, task7_nginx_conf_template.png, task7_my_playbook_web_deploy.png, task7_ansible_play_web_deploy.png, task7_php_https_browser.png

Task 8 – Docker & Docker Compose
Wrote a playbook to install Docker and the Docker Compose CLI plugin.

Verified system architecture using Ansible facts and uname -m.

Screenshots: task8_terraform_destroy_old.png, task8_terraform_apply_docker_instance.png, task8_terraform_output_new_ip.png, task8_hosts_docker_servers.png, task8_my_playbook_docker.png, task8_ansible_play_docker.png, task8_docker_ps_remote.png

Task 9 – Gitea Stack Deployment
Deployed a Gitea + PostgreSQL stack using a compose.yaml file.

Updated AWS Security Groups via Terraform to allow traffic on port 3000.

Screenshots: task9_my_playbook_add_user_to_docker.png, task9_project_vars.png, task9_my_playbook_deploy_containers.png, task9_compose_yaml.png, task9_ansible_play_gitea.png, task9_sg_ingress_3000.png, task9_terraform_apply_sg_3000.png, task9_gitea_browser.png

Task 10 – Terraform Automation (null_resource)
Integrated Ansible into the Terraform lifecycle using null_resource and local-exec.

Implemented a "wait for SSH" task in Ansible to ensure instance readiness.

Screenshots: task10_null_resource_main_tf.png, task10_terraform_destroy_before_null.png, task10_terraform_apply_with_local_exec.png, task10_my_playbook_wait_for_ssh.png, task10_terraform_apply_after_wait.png, task10_app_browser_post_null_resource.png

Task 11 – Dynamic Inventory
Configured the aws_ec2 plugin in ansible.cfg.

Enabled dynamic host discovery based on AWS tags.

🧹 Cleanup
To avoid unnecessary AWS charges, the infrastructure was destroyed after completion:

Bash

terraform destroy -auto-approve
📤 Submission Details
Repository:  areej-10-open-ended-lab
