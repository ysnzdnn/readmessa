## Auto Shutdown and Auto Start of Azure Vm

Purpose of this Readme file is showing the people how to start and shut down automatically virtual machines of Microsoft Azure.

## Outlines

Part 1 - Creating the new deployment for the start and stop.

Part 2- Finding resource groups at Microsoft Azure.

Part 3 - Setting up the stop schedule of Vm's.

Part 4 - Setting up the start schedule of Vm's.


## Part 1 - Creating the new deployment for the start and stop.

As a first step, you need to open this link (https://github.com/microsoft/startstopv2-deployments/blob/main/README.md).

- And after that you need to click on  "Deploy The Azure" button which is under **Global Users**.

- At the opening Section you are going to choose "StartStopv2" as a plan. After that you will click on the "Create" button.

- We are going to see a new tab which is includes two tab one of it name is Project Details and otheris Instance Details. At this Section youl will choose your subscription and you will prepare your instance details, let's make an example together in the following section.  

# Example for Instance Details and Product Details Part -

- in the *Product Detials* part you can choose your subscription. If you have a one subscription which can be 'Azure subscribtion 1'will be coming automatically on this part.

- *Instance Details* this part consists of the details and you can choose the region and you can give a name for your resource.

 For this example, we will choose and give name like the followings.

Region - West US
Resource Group Name - StartStopDemo
Azure Function App Name - StartStopDemoFA
Application Insights Name - StartStopDemoAI
Application Insight Region - West Us
StorageAccountName - startstopdemosa

and optionally you may add E-Mail Adress.

- After completing the section we are going to click on review+create button and see if we have problem.

- At the opening section we will see the **Basics** of our Deployment then we can click the create button.


## Part 2 - Finding Resource Groups

- In this section, we will learn how to use the deployment that we have created.

- First of all, in the Azure you can see the portal menu by clicking the 3 lines button whisch you can see left top corner of the screen. 
- You should go to the resource group section which you can find on the portal menu or you can use search engine of Microsoft Azure.
- in the Resource Group section you can see you resource groupes and at that section you should see a resource group named "StartStopDemo" we will select this resource  group.


## Part 3 - Setting up the stop schedule of Vm's.

- After selecting "StartStopDemo" resource group we need to find a logic app named of **ststv2_vms_Scheduled_stop** and type is **logic app**.

- Logic app we need to *Edit* this app. So, at the showing up screen find the *Edit* button which is a pen image near of it, click on it.

 - You will see two section one of it name is "Recurrence" and the other is "Function-Try"

 - At the coming up screen click on Function-Try part and the opening section you will see a section that name is scheduled, also click on it.
 
 - At the opening part there is a two section. One of it name is Request Body and the other is Add new parameter.

at the request body section there is a function something like the following section. 


"Resource Groups":[
 

    "/subscriptions/1111111-2222-3333-4444-55555555555/resourceGroups/rg1",
      
]


 - After Finding that part you need to change this part with your subscription id and your resource group name. as to swap 11111-222-333-4444-5555555 part change with your subscription id.

 - And you will change rg1 part with your resource group name.

 *You can find your subscription id at the Virtual Machines part by clicking the virtual machine that you want to auto start and stop.*

 *You can find your resource group on resource group home screen or vm's essentials part which you can see when you open your vm.*


 - After all the changes has been complete your resource group has to be something like that.



"Resource Groups":[
 

       "/subscriptions/4a8e0f70-8db3-4fc5-b8b3-6442a64bc027/resourceGroups/VM-FIRST1",
      
]

!! Note: You can use a lot of VM. If you are going to add a new VM, then you have to add its subscription id and resource group as new line in Resource Groups part. !!

# Example for the note #


"Resource Groups":[
 
   
 
       "/subscriptions/4a8e0f70-8db3-4fc5-b8b3-6442a64bc027/resourceGroups/VM-FIRST1",

         "/subscriptions/4a8e0f70-8db3-4fc5-b8b3-6442a64bc027/resourceGroups/vm2"
]

 - And if you work on Classic Vm you need to change ; (If you are beginner keep it as false.)

   "EnableClassic": false, to
   "EnableClassic": true,

 - After preparing the Function-Try section you will click on save button that you can find on left top corner.

 - Now we handled with Function-Try part. After that you are going to open "Recurrence" section.

 - Then you will set-up your Interval, Frequency, Time Zone, Hour and Minutes settings.

 - Also if you need more parameters.You can add it from the Add new parameter part. Which is below in the Recurrence section.
 
 - You can see your settings in the Preview section.

 # for Example 
 
 - if you want to run the Stop scheduler at 18.30 everyday;
    
 - Interval: 1 Frequency: Day
 - Time Zone : UTC +2
 - At these hours: 18
 - At these minutes: 30
  
 - is the setup.



 - After you configure your recurrence section you will save it again by clicking on it.
 
 - And you will see a completed information pop-up right top or you can see this in Notifications.

 - After your configurations, you will open "ststv2_vms_Scheduled_stop" app page and you will see *Enable* button at the same level with edit button and a start image near of it.

 - Click on this button and start your stop scheduler.




# Part 4 - Setting up the start schedule of Vm's.

- After selecting "StartStopDemo" resource group we need to find a logic app named of **ststv2_vms_Scheduled_start** and type is **logic app**.

- Logic app we need to *Edit* this app. So, at the showing up screen find the *Edit* button which is a pen image near of it, click on it.

 - You will see two section one of it name is "Recurrence" and the other is "Function-Try".

 - Let's open "Recurrence" section for this time.

 - Then you will set-up your Interval, Frequency, Time Zone, Hour and Minutes settings.

 - Also if you need more parameters.You can add it from the Add new parameter part. Which is below in the Recurrence section.
 
 - You can see your settings in the Preview section.

 - After completing your time zone you can open Function-Try section.

 - At the coming-up screen you will delete the Resource Groups parameter this time.

 - you will delete "ResourceGroups":[


         "/subscriptions/1111111-2222-3333-4444-55555555555/resourceGroups/rg1",

 ]
 this part.

 and add this "VmLists": [] instead of "ResourceGroups:[]" parameter.

 - After the adding, you are going to add a part of your VM's URL that you want to start auto schedule.

# Clarify
 
    
      https://portal.azure.com/#@blablabla/resource/subscriptions/4a8e0f70-8db3-4fc5-b8b3-6442a64bc027/resourceGroups/VM-FIRST1/providers/Microsoft.Compute/virtualMachines/vmFirst1/overview
 - You are going to copy after the resource part and before the overview part of the URL. Then, add it to the vmLists parameter.
 - The Copy that has been taken from the URL of VM.

        /subscriptions/4a8e0f70-8db3-4fc5-b8b3-6442a64bc027/resourceGroups/VM-FIRST1/providers/Microsoft.Compute/virtualMachines/vmFirst1/overview

--Shown below.--

"VmLists":[

        "/subscriptions/4a8e0f70-8db3-4fc5-b8b3-6442a64bc027/resourceGroups/VM-FIRST1/providers/Microsoft.Compute/virtualMachines/vmFirst1",

 ]


 !! Note: You can use a lot of VM. If you are going to add a new VM, then you have to add its URL link as the same way and add it to VmLists separately. !!

- And if you work on Classic Vm you need to change ; (If you are beginner keep it as false.)

   "EnableClassic": false, to
   "EnableClassic": true,


 - After preparing the "Function-Try" and "Recurrence" sections you can save it by clicking the save button that is on left top corner of the white screen.
 
 - After the saving go back to logic app screen and press *Enable* button to enable it.


 
   





 
