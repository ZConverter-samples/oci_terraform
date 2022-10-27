OCI Terraform
============

> Before You Begin
> 
> Prepare
> 
> Install Terraform Data
> 
> Start Terraform



## Before You Begin
To successfully perform this tutorial, you must have the following:

   * An Oracle Cloud Infrastructure account. [See Signing Up for Oracle Cloud Infrastructure](https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/signingup.htm)
   * A MacOS, Linux, or Windows environment:
   * MacOS
   * Linux (Any distribution)
      - You can install a Linux VM with an **Always Free** Compute shape, on Oracle Cloud Infrastructure:
         +  [Install an Ubuntu VM](https://docs.oracle.com/iaas/developer-tutorials/tutorials/helidon-on-ubuntu/01oci-ubuntu-helidon-summary.htm#create-ubuntu-vm)
         +  [Install an Oracle Linux VM](https://docs.oracle.com/iaas/developer-tutorials/tutorials/apache-on-oracle-linux/01oci-ol-apache-summary.htm#create-oracle-linux-vm)
   * Oracle Cloud Infrastructure Cloud Shell:
      -  [Cloud Shell](https://docs.oracle.com/iaas/Content/API/Concepts/cloudshellintro.htm)
   * Windows 10
      -  [Windows Subsystem for Linux](https://docs.microsoft.com/windows/wsl/install-win10) (WSL)
      -  [Git for Windows](https://gitforwindows.org/) to access a Linux VM.



## Prepare
Prepare your environment for authenticating and running your Terraform scripts. Also, gather the information your account needs to authenticate the scripts.

### Install Terraform
   Install the latest version of Terraform **v1.3.0+**:

   1. In your environment, check your Terraform version.
      ```script
      terraform -v
      ```

      If you don't have Terraform **v1.3.0+**, then install Terraform using the following steps.

   2. From a browser, go to [Download Latest Terraform Release](https://www.terraform.io/downloads.html).

   3. Find the link for your environment and then follow the instructions for your environment. Alternatively, you can perform the following steps. Here is an example for installing Terraform v1.3.3 on Linux 64-bit.

   4. In your environment, create a temp directory and change to that directory:
      ```script
      mkdir temp
      ```
      ```script
      cd temp
      ```

   5. Download the Terraform zip file. Example:
      ```script
      wget https://releases.hashicorp.com/terraform/1.3.3/terraform_1.3.3_linux_amd64.zip
      ```

   6. Unzip the file. Example:
      ```script
      unzip terraform_1.3.3_linux_amd64.zip
      ```

   7. Move the folder to /usr/local/bin or its equivalent in Mac. Example:
      ```script
      sudo mv terraform /usr/local/bin
      ```

   8. Go back to your home directory:
      ```script
      cd
      ```

   9. Check the Terraform version:
      ```script
      terraform -v
      ```

      Example: `Terraform v1.3.3 on linux_amd64`.

### Create API-Key
   If you created API keys for the Terraform Set Up Resource Discovery tutorial, then skip this step.

   Create RSA keys for API signing into your **Oracle Cloud Infrastructure account**.

   1. **Log in to the Oracle Cloud site and access the user portal.**

      ![Login](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/login.png)  

   2. **Enter the User menu.**

      ![Account User](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/user_account.png)  

   3. **Choice User Account Name to use.**

      ![Account Users](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/user_account_choice.png)

   4. **Click api-key in the lower left resource and click add api key**

      ![Api-Key](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/api_key_add.png)

   5. **Under API Key Pairing, click Download Private Key and Download Public Key, and then click the Add button. If there are more than three API Key, Delete API Key or use another User Account Name.**

      ![Api-Key](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/api_key_download_key_file.png)

   7. **Copy the results from Configuration File Preview onto the notepad.**

      ![Configuration](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/api_key_copy.png)
   
   8. **Select Networking from the menu, then select Virtual Cloud Networks**

      ![Networking-Virtual Cloud Network](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/click_vcn.png)
   
   9. **Choice VCN User Account Name to use**

      ![Select VCM User Account Name](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/click_vcn_zcon.png)

   1. **Choice Subnets Name to use**

      ![Select Subnets Name](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/click_subnet.png)

   1. **Copy the Subnet OCID onto the notepad**

      ![Subnet OCID](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/copy_subnet_ocid.png)

   1. **Result**

      ![Result](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/download_result.png)

  

## Install OCI Terraform Data
   Install the **terraform data** you need to make your OCI vm.

   1. **Download [Terraform data](https://github.com/zconverter/ZCM-Baisc/raw/master/image/oci_terraform/oci_terraform.zip)**

   2. **Unzip OCI Terraform data**

      ![OCI terraform data](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/unzip_oci_terraform.png)



## Start Terraform

   1. **Edit a vars.tfvars File you want to create VM**

      ![vars.tfvars](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/var_tfvar.png)

      * vars.tfvars data info:
         + tenancy : Use the tenancy noted in API Key creation.
         + user : Use the user noted in API Key creation.
         + key_file : Use the absolute path of private_key downloaded from API Key generation.
         + fingerprint : Use the fingerprint noted in API Key creation.
         + region : Use the region noted in API Key creation.
         + compartment : Tenancy or compartment for that account
         + shape : 
            - Flexible Shapes : VM.Standard.E3.Flex, VM.Standard.E4.Flex, VM.Optimized3.Flex, VM.Standard.A1.Flex
            - Standard Shapes : VM.Standard2.1, VM.Standard2.2, VM.Standard2.4, VM.Standard2.8, VM.Standard2.16, VM.Standard2.24
         + os :
         + os_version : 
            | | Windows2019 | Windows2016 | Windows2012 R2 | Linux8 | Linux7.9 | Linux6.10 | centos8 | centos7 | centos8 | ubuntu20.04 | ubuntu18.04 | ubuntu16.04 |
            |-|-------------|-------------|----------------|--------|----------|-----------|---------|---------|---------|-------------|-------------|-------------|
            | OS | Windows | Windows | Windows | Oracle Linux | Oracle Linux | Oracle Linux  | CentOS | CentOS | CentOS | Canonical Ubuntu | Canonical Ubuntu | Canonical Ubuntu |
            | OS_Version | Server 2019 Standard | Server 2016 Standard | Server 2012 R2 Standard | 8 | 7.9 | 6.10 | 8 | 7 | 6 | 20.04 | 18.04 | 16.04 |
         + block_volume_count : Number of volumes on server you want to create
         + block_volume_size : Size of volume on server you want to create
         + block_volume_diskplay_name : Name of volume on server you want to create
         + blcok_volume_device_path : Specifies the path to the disk when you add it to the Linux family operating system.
         + diskplay_name : Name of Server you want to
         + subet_ocid : Use the account's subnet_ocid.
         + user_data_path :
            - Enter the path to the txt file in the scripts folder of the downloaded oci_terraform. 
            - Use the file oci_linux_cloud_init_txt for Linux-like operating systems and the file oci_windows_cloud_init_txt for Windows-like operating systems.
         + ssh_public_key_path : Linux-like operating systems require the file path of the user's ssh_public key.
         + ocpus : You must enter the number of CPUs when using Flexible_shape. The range is from 1 to 64.
         + memory_in_gbs : When using Flexible_shape, you must select memory capacity. The range is from cpu count to 1024.

   2. **Start CMD**

      ![cmd](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/start_cmd.png)

   3. **Go to the file path of Terraform.exe and Initialize the working directory containing the terraform configuration file.**

      ```script
      terraform.exe -chdir={terraform data file path} init
      ```

      **Note**
      * -chdir : The usual way to run Terraform is to first switch to the directory containing the `.tf` files for your root module (for example, using the `cd` command), so that Terraform will find those files automatically without any extra arguments.

      ![terraform init](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/tf_init.png)
   
      ![terraform init result](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/tf_init_result.png)


   4. **Creates an execution plan. By default, creating a plan consists of:**

      * Reading the current state of any already-existing remote objects to make sure that the Terraform state is up-to-date.
      * Comparing the current configuration to the prior state and noting any differences.
      * Proposing a set of change actions that should, if applied, make the remote objects match the configuration.

      ```script
      terraform.exe -chdir={terraform data file path} plan -var-file={vars file with user specified name}
      ```

      **Note**
      * -var-file : Sets values for potentially many [input variables](https://www.terraform.io/docs/language/values/variables.html) declared in the root module of the configuration, using definitions from a ["tfvars" file](https://www.terraform.io/docs/language/values/variables.html#variable-definitions-tfvars-files). Use this option multiple times to include values from more than one file.
      * The file name of vars.tfvars can be changed.

      ![terraform plan](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/tf_plan.png)

   5. **Executes the actions proposed in a Terraform plan.**

      ```script
      terraform.exe -chdir={terraform data file path} apply -var-file={vars file with user specified name} -auto-approve
      ```
      **Note**
      * -auto-approve : Skips interactive approval of plan before applying. This option is ignored when you pass a previously-saved plan file, because Terraform considers you passing the plan file as the approval and so will never prompt in that case.

      ![terraform apply](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/tf_apply.png)

   6. **Result**

      ![terraform apply result](https://raw.githubusercontent.com/zconverter/ZCM-Baisc/master/image/oci_terraform/result_terraform%20apply.png)
