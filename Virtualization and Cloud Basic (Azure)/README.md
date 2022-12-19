<h2>Azure Home Tasks</h2>
<head>
<h3>Prerequisites</br>
1.	Create azure subscription</br>
2.	Create azure devops organization</br>
3.	Read information about github flow branching strategy</br>
4.	terraform should be installed </br>
5.	Terraform knowledge is also required to do the stuff</br>
6.	Az cli should be installed</br></h3>
<h2>Homework Part 1 – Configure application</h2><h3>
1.	Create a service connection in a Azure DevOps project to your subscription</br><img src="https://github.com/korotetskiy/img/blob/main/azure1-1.png"></br>
2.	Find a .net pet project for the experiments</br>
3.	Build your app locally .net project via dotnet tool. dotnet restore/build/run</br>
4.	Create an Azure DevOps repo. You can use import repository to import from existing source control version like github.</br><img src="https://github.com/korotetskiy/img/blob/main/azure1-4-repo.jpg"></br>
5.	Create a branching policy for you application. Added yourself as a reviewer. As branching strategy use a github flow (It will be applied by default when you strict commit to your main branch)</br><img src="https://github.com/korotetskiy/img/blob/main/azure1-5.png"></br></h3>
<h3>Part 2 – Configure a pipeline to deploy infrastructure</h3>
<h4>Below is describing on how to do it via terraform. If you want to use terraform you need to create service connection in manual way. Otherwise you won’t be able to deploy your iac – Navigate to the last section.</h4><img src="https://github.com/korotetskiy/img/blob/main/azure-pipleline.png">
<h3>Terraform storage account</br>
1.	Create a separate resource group and deploy azure storage account<img src="https://github.com/korotetskiy/img/blob/main/azure2-1.png"></br>
2.	Create a container with the name “tfstate” and remember the name "tfstate"  use portal settings. In this storage account you will be store your tf state file<img src="https://github.com/korotetskiy/img/blob/main/azure2-2.png"> </h3>   
<h3>Terraform preparation</br>
1.	Create another repo to store devops code</br>
2.	Create a folder terraform</br>
3.	Add app service implementation</br> 
4.	Integrate application insights with app service</br>
<img src="https://github.com/korotetskiy/img/blob/main/azure-pr1.png">
5.	Updated backend "azurerm" according to the guide </br><img src="https://github.com/korotetskiy/img/blob/main/azure-tp.png">
6.	Run az login or Connect-AzAccount to connect the azure subscription from your local</br>
7.	Run terraform apply to deploy infrastructure</br><img src="https://github.com/korotetskiy/img/blob/main/azure_rtf1.png"></h3>
Important note: Use only freshest version of tf module like https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/windows_web_app
</br>Important note: Don’t forget to destroy your application once completed
<h3>Create a terraform pipeline</br>
1.	Create a yaml pipeline with the following steps: terraform install, terraform init, terraform plan/apply. Plan is an optional one</br>
2.	Inside yaml pipeline add trigger to main branch. The scenario – when main is updated, pipeline should run automatically.
3.	Added 3 steps – terraform install, terraform init, terraform plan/apply. Plan is an optional one. You may add it as 4th step</br></br><img src="https://github.com/korotetskiy/img/blob/main/azure_run_tf.png"><img src="https://github.com/korotetskiy/img/blob/main/azure_run_tf2.png"><img src="https://github.com/korotetskiy/img/blob/main/azure_run_tf1.png">
</br></br>Part 3 – Create a deploy pipeline to app service</br>
1.	Add yml pipeline to the application folder</br>
2.	Your pipeline structure should contain 2 stages. 1st – build, create zip archieve, and publish an artifact. 2nd – download an artifact and deploy it to azure app service 
3.	To deploy .zip to app service use azure app service deployment task</br></h3>
Don’t forget to grant access on the subscription level for your enterprise application (service principal)
