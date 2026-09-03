
Hey so we have a new task the task is basically which are:

1 .Create implmentation plan for android dev coworker and it's ai agent in such a way where they know what to do how to how to do and where to do but without giving them the exact code place context caus we also dont have it just tell them the requirement and the flow what is required and to be needed.

The mobile app i will not be working on mobile app and i dont have the codebase of that i have to create a plan to basically give context to my android dev teammate who will be working on it remotely and i have to give him the requirement document understanding and how to implement it implementation plan for his ai agent to one shot implement it all basically in one for both of them ai agent and coworker.

Tell in such a way where it will know what to exactly do where to do even how to do but tell it to find those plases manually like i cant exactly tell the componenet but can tell the phase where that component shows type of that component and what text it have that type shit so basically a high level overview of the req and changes need to be done but now exactly how and where to do it in code caus we dont have it.

2 . create a implemnetation plan for me to implement my side of the changes majory in the backend but some changes in the frontend.

check the @PROJECTS.md file for the project context and flow of the application in real world and its connect with the mobile app.

Requirements to be implemented in the project.

So as you may know till this point how the project is working so .

when from place a LTS is going from a Place A to Place B during a drawl.

This place B wants in there software to basically have automation and history mangement.

How :

Basically there is will be a entry gate use which will have the mobile phone with the app in it which will be connected to there LAN and there server which is this projects server its in a safe secure lan environment.

now the gate use have a special type of login in the app using the "EXPORT" button on the home login screen user clicks on that fill the password clicks proceed then have a button "SCAN NFC CARD" user scan the nfc card and see all the data from the nfc card there we want to have a button on top which will basically be a text input optional one which will basically be for telling that from which place here Place A this data came from this will be used in the AMK inventory stock history managent to tell what came from where so this will tell that this entire LTS or basically vechile which came with the AMK came from here so we can track history right.

then the box we are current showing after scanning the card even though the card have all the details all the data in json for which is getting imported we are showing them the vechile number driver name unit checkout time and scanned at which is basically when they got out from the Place A.

So in this box what we want to show the details about the lts which is in the card thing like from which shed or location this came from what is the amk no what is the Nomenclature how much given and then the main part after it that give a drop down which will be basically what location now you want to store it at what shed give that dropdown and fill that dropdown with options from the api

( Note : Check the codebase and tell me is there any api which will get me the list of locations like for a dropdown all at once for the From the amk check how the fuck we are getting it here  [ManageAMKQuantitySearch.jsx#L60-81](fileLineRange;file:///home/prince/code/office/projects/dms/frontend/src/manageAMKQuantity/ManageAMKQuantitySearch.jsx#L60-81) waht we want is a proper list of location from api which the mobile dev can use so if there is write that in the plan for the mobile dev is there is not then we have to create one and then add that route and the data format it will give back. so they can integrate it all seemlessaly and get list of all possible location feeded in the system though the existing AMK sheets and amount or how ever they have added ).

and also a input field to add there custom so they can add a custom location which is not in the db AMK's so what i told add a input from location where this LTS came from on top and then show the deatils of each AMK properly which is comming from the NFC Card and then a dropdown which will call api to get all existing location but can also add there custom location in that to tell where this LOT is getting stored

Then there is a "EXPORT SELECTED" button which Make is "EXPORT & Auto Sync" this will be the button which will export a excel sheet feature already implemented but in that sheet before it was giving the "loc" or "shed_location" or "shed_loc" field there is no consistency caus the application is getting used at mulitple places and they all have there custom diff conventions so add a regex to find find that filed basically and in that filed before we wer adding the location of the prev Place A storage location basically where it they had it stored in the previous place but now we want the newly added locations to be at that those places. 

Now the sync part basically what we will do is that we will be creating the export/data_sync api route this will basically be a route which will send this data to the connected server basically the Place B server from that Place B phone from the entery gatekeepr who will be exporting this sheet this mobile will make api call to the server and get this data stored along side maintaining history and stored means basically auto import the amk too store the data so basically will be using the import excel type or bulk upload feature which already exists in the backend codebase to import this new data with updated location of where to store and we will also store in history about history i will tell in the part 2 how will it be implmented it will just be a backend module and frontend no mobile it will store old location which will user fill also all the data the user is sending from the frontend baiscally the entire json but it must have the new locaiton old location and other important field we will store it as a unstructured json basically proper detail of which driver which lts anything which is important it will send it all and save it directoly as json important fields on top and other on bottom and then we will show it in the desktop frontend. Now when the user clicked on export and sync data he got the latest excel with latest location and synced data in the server automatically and created history log of that but between that phace we want a confirmation modal only in the case where the user does not fill the prev location field the lable for that input should be "parent Depot name" then a input now if the user does not fill this or any of the current locations then show them modal with detials that you have not filled this field's this field type shit and also telling that you have added a custom location if the user have not selected from the dropdown ( note the parent locaiton one will just be a normal text input not a dropdown mind you that only the new location will be dropdown with also option to custom write new location make it like a button in the end of the dropdown of add location and there they can addd a location after clickign that button by filling the name in a modal which will popup with new location name input ) but talking about the confirmation modal of not field prev or any of the new location just show a warning modal that this is the case do you want to continue and then a continue or cancel button so the user can continue or go back and edit the form. also give a cross option to close the modal or if the user clicks on the back button it should click then to not like close or back the application on back button click and remove all the progress.
make it match the ui and make it look good 
so this is all the work for mobile app .

Now for requirment 2 

Basically create a proper plan to implment a backend a frotnend api and all that shit and then we will implmenent it all but for now clearfy the data strucutre for the data they have to send for history and import and what data they will get in the location listing and what api route to call for doing both the geting list and updating sync and history thing auto impport on the button click and history one should be cymantenious on the same api no diff api calls for now but make them two diff fuction be be reused in the future.

as you might have understood till this point i dont have much idea about the mobile app or nfc card internally stored data caus its hanedeled by mobile too and a little bit by backend but it depends on the api route and all 

so you have give the insturctions for there ai in such a way where it can find out from there codebase of mobile app and the backend but they will not have the latest updated baceknd code caus we will implenent it in a diff seperate remote branch so confirmat that to there ai modal that dont create or do anythign in there backend automatically if some thing does not exists like some api route which we have not created till now and these are the assumptions and these are the convention and these are the requirements and figure out other parts by its own but one thing is that give them proper data sturce which they will receive and have to send by or to the baceknd respectively so we both are on the same page and you implementation of the baceknd then should be same as you have told them to impletne in the mobile app in the doc other wise it will not work.


the history system will kind of work like the activity logs module in teh fornend chekc that out to understand it proeprly.


Work on the 1st part first and then second
