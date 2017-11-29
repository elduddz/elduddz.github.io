witadmin importwitd /collection:collection /p:project /f:epic.xml

witadmin exportcategories /collection:collection /p:project /f:exportcategories.xml

<CATEGORY name="Epic Category" refname="Microsoft.EpicCategory"> 
<DEFAULTWORKITEMTYPE name="Epic" /> 
</CATEGORY>

witadmin importcategories /collection:collection /p:project /f:exportcategories.xml

cd ..\process

witadmin exportprocessconfig /collection:collection /p:project /f:exportProcessConfiguration.xml

Something else...

witadmin importprocessconfig /collection:collection /p:project /f:exportProcessConfiguration.xml