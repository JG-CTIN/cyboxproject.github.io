---
layout: flat
title: Object Relationships
---

This page contains a listing of some of the available CybOX Object → Object
relationships (from the [ObjectRelationshipVocab-1.1](http://stixproject.github.io/data-model/1.1.1/cyboxVocabs/ObjectRelationshipVocab-1.1/) vocabulary), and adds some additional context for each relationship. This includes a richer definition,
a listing and description of the Objects that the relationship is most applicable
to (note that it may be applicable to others not covered here), its inverse 
(if existing), and an example XML snippet that demonstrates the
relationship in use.

# Overview

|Name|Inverse|Applicable Objects (Source)|Applicable Objects (Related)|
|----|-------|---------------------------|----------------------------|
|[Created](#Created)|[Deleted](#Deleted), [Killed](#Killed)|[Archive File], [Process]|[File], [Process], [Mutex], [Win Registry Key], [Win Service], [Win Thread]|
|[Created_By](#Created_By)|[Deleted_By](#Deleted_By), [Killed_By](#Killed_By)|[File], [Process], [Mutex], [Win Registry Key], [Win Service], [Win Thread]|[Archive File], [Process]|
|[Deleted](#Deleted)|[Created](#Created)|[Process]|[File], [Mutex], [Win Registry Key], [Win Service]|
|[Deleted_By](#Deleted_By)|[Created_By](#Created_By)|[File], [Mutex], [Win Registry Key], [Win Service]|[Process]|
|[Modified_Properties_Of](#Modified_Properties_Of)|n/a|[Process]|[File], [Win Registry Key], [Win Service]|
|[Properties_Modified_By](#Properties_Modified_By)|n/a|[File], [Win Registry Key], [Win Service]|[Process]|
|[Downloaded_From](#Downloaded_From)|n/a|[File]|[URI], [Domain Name], [Address], [Hostname]|
|[Downloaded_To](#Downloaded_To)|[Uploaded_To](#Uploaded_To)|[URI], [File]|[File]|
|[Downloaded](#Downloaded)|[Uploaded](#Uploaded)|[Process]|[File]|
|[Downloaded_By](#Downloaded_By)|[Uploaded_By](#Uploaded_By)|[File]|[Process]|
|[Uploaded](#Uploaded)|[Downloaded](#Downloaded)|[Process]|[File]|
|[Uploaded_By](#Uploaded_By)|[Downloaded_By](#Downloaded_By)|[File]|[Process]|
|[Uploaded_To](#Uploaded_To)|[Downloaded_To](#Downloaded_To)|[File]|[URI], [Domain Name], [Address], [Hostname]|
|[Sent_To](#Sent_To)|[Received_From](#Received_From)|[File]|[Address]|
|[Received_From](#Received_From)|[Sent_To](#Sent_To)|[File]|[Address]|
|[Values_Enumerated](#Values_Enumerated)|n/a|[Process]|[Win Registry Key]|
|[Values_Enumerated_By](#Values_Enumerated_By)|n/a|[Win Registry Key]|[Process]|
|[Killed](#Killed)|[Created](#Created)|[Process]|[Process], [Win Thread]|
|[Killed_By](#Killed_By)|[Created_By](#Created_By)|[Process], [Win Thread]|[Process]|
|[Locked](#Locked)|[Unlocked](#Unlocked)|[Process]|[File]|
|[Locked_By](#Locked_By)|[Unlocked_By](#Unlocked_By)|[File]|[Process]|
|[Unlocked](#Unlocked)|[Locked](#Locked)|[Process]|[File]|
|[Unlocked_By](#Unlocked_By)|[Locked_By](#Locked_By)|[File]|[Process]|
|[Listened_On](#Listened_On)|n/a|[Process]|[Port], [Network Socket]|
|[Renamed_From](#Renamed_From)|n/a|[File]|[File]|
|[Renamed_To](#Renamed_To)|n/a|[File]|[File]|
|[Renamed](#Renamed)|n/a|[Process]|[File]|
|[Renamed_By](#Renamed_By)|n/a|[File]|[Process]|
|[Moved_From](#Moved_From)|n/a|[File]|[File]|
|[Moved_To](#Moved_To)|n/a|[File]|[File]|
|[Moved](#Moved)|n/a|[Process]|[File]|
|[Moved_By](#Moved_By)|n/a|[File]|[Process]|
|[Copied_From](#Copied_From)|n/a|[File]|[File]|
|[Copied_To](#Copied_To)|n/a|[File]|[File]|
|[Copied](#Copied)|n/a|[Process]|[File]|
|[Copied_By](#Copied_By)|n/a|[File]|[Process]|
|[Contains](#Contains)|n/a|[File], [Archive File], [Email Message], [URI], [DNS Record], [ARP Cache], [URL History], [Win Registry Key]|[File], [Link], [Domain Name], [Address], [URI], [Win Registry Key]|
|[Contained_Within](#Contained_Within)|n/a|[File], [Link], [Domain Name], [Address], [URI], [Win Registry Key]|[File], [Archive File], [Email Message], [URI], [DNS Record], [ARP Cache], [URL History], [Win Registry Key]|
|[Extracted_From](#Extracted_From)|n/a|[File], [URI], [Link]|[File], [Archive File], [Email Message]|
|[Connected_To](#Connected_To)|n/a|[Process]|[Address], [Socket Address], [Hostname], [Network Socket]|
|[Parent_Of](#Parent_Of)|[Child_Of](#Child_Of)|[Process]|[Process], [Win Thread]|
|[Child_Of](#Child_Of)|[Parent_Of](#Parent_Of)|[Process], [Win Thread]|[Process]|
|[Redirects_To](#Redirects_To)|n/a|[URI], [Domain Name]|[URI], [Domain Name]|
|[Suspended](#Suspended)|[Resumed](#Resumed)|[Process]|[Process], [Win Thread]|
|[Suspended_By](#Suspended_By)|[Resumed_By](#Resumed_By)|[Process], [Win Thread]|[Process]|
|[Paused](#Paused)|[Resumed](#Resumed)|[Process]|[Win Service]|
|[Paused_By](#Paused_By)|[Resumed_By](#Resumed_By)|[Win Service]|[Process]|
|[Resumed](#Resumed)|[Suspended](#Suspended), [Paused](#Paused)|[Process]|[Process], [Win Thread], [Win Service]|
|[Resumed_By](#Resumed_By)|[Suspended_By](#Suspended_By), [Paused_By](#Paused_By)|[Process], [Win Thread], [Win Service]|[Process]|
|[Wrote_To](#Wrote_To)|[Read_From](#Read_From)|[Process]|[Process], [File], [Pipe], [Win Mailslot]|
|[Written_To_By](#Written_To_By)|[Read_From_By](#Read_From_By)|[Process], [File], [Pipe], [Win Mailslot]|[Process]|
|[Read_From](#Read_From)|[Wrote_To](#Wrote_To)|[Process]|[Process], [File], [Pipe], [Win Mailslot]|
|[Read_From_By](#Read_From_By)|[Written_To_By](#Written_To_By)|[Process], [File], [Pipe], [Win Mailslot]|[Process]|
|[Allocated](#Allocated)|[Freed](#Freed)|[Process]|[Memory], [Win Memory Page Region]|
|[Allocated_By](#Allocated_By)|[Freed_By](#Freed_By)|[Memory], [Win Memory Page Region]|[Process]|
|[Freed](#Freed)|[Allocated](#Allocated)|[Process]|[Memory], [Win Memory Page Region]|
|[Freed_By](#Freed_By)|[Allocated_By](#Allocated_By)|[Memory], [Win Memory Page Region]|[Process]|
|[Opened](#Opened)|[Closed](#Closed)|[Process]|[File], [Win Filemapping], [Mutex], [Semaphore], [Port], [Win Event], [Win Critical Section], [Win Handle], [Win Registry Key], [Win Service]|
|[Opened_By](#Opened_By)|[Closed_By](#Closed_By)|[File], [Win Filemapping], [Mutex], [Semaphore], [Port], [Win Event], [Win Critical Section], [Win Handle], [Win Registry Key], [Win Service]|[Process]|
|[Closed](#Closed)|[Opened](#Opened)|[Process]|[File], [Win Filemapping], [Port], [Win Handle], [Win Registry Key]|
|[Closed_By](#Closed_By)|[Opened_By](#Opened_By)|[File], [Win Filemapping], [Port], [Win Handle], [Win Registry Key]|[Process]|
|[Characterizes](#Characterizes)|n/a|[File], [DNS Record], [WHOIS]|[Artifact], [Domain Name]|
|[Characterized_By](#Characterized_By)|n/a|[Artifact], [Domain Name]|[File], [DNS Record], [WHOIS]|
|[Resolved_To](#Resolved_To)|n/a|[Domain Name], [Hostname], [Address]|[Domain Name], [Hostname], [Address]|
|[Sub-domain_Of](#Sub-domain_Of)|[Supra-domain_Of](#Supra-domain_Of)|[Domain Name]|[Domain Name]|
|[Supra-domain_Of](#Supra-domain_Of)|[Sub-domain_Of](#Sub-domain_Of)|[Domain Name]|[Domain Name]|
|[FQDN_Of](#FQDN_Of)|n/a|[Domain Name]|[Domain Name], [Hostname]|
|[Dropped](#Dropped)|n/a|[File]|[File]|
|[Dropped_By](#Dropped_By)|n/a|[File]|[File]|

## <a name="Created"></a> "Created"

The **source Object** *Created* the **related Object**. Applicable to a wide range of Objects, particularly in the context of a [Process] that creates other Objects.

### Inverse

[Deleted](#Deleted)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Archive File]|[File]|A self-extracting archive file created a file upon extraction.|
|[Process]|[File]|A process created a file during its execution.|
|[Process]|[Process]|A process created another process during its execution.|
|[Process]|[Win Registry Key]|A process created a Windows registry key or registry key value during its execution.|
|[Process]|[Win Service]|A process created a Windows service during its execution.|
|[Process]|[Mutex]|A process created a mutex during its execution.|
|[Process]|[Win Thread]|A process created a Windows thread during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Created</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Created_By"></a> "Created_By"

The **source Object** was *Created by* the **related Object**. Applicable to a wide range of Objects, particularly in the
context of Objects that were created by a [Process].

### Inverse

[Deleted_By](#Deleted_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Archive File]|A file was created by a self-extracting archive file as part of its extraction operation.|
|[File]|[Process]|A file was created by a process during its execution.|
|[Process]|[Process]|A process was created by another process during its execution.|
|[Win Registry Key]|[Process]|A Windows registry key or registry key value was created by a process during its execution.|
|[Win Service]|[Process]|A Windows service was created by a process during its execution.|
|[Mutex]|[Process]|A mutex was created by a process during its execution.|
|[Win Thread]|[Process]|A Windows thread was created by a process during its execution.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Created_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Deleted"></a> "Deleted"

The **source Object** *Deleted* the **related Object**. Applicable to a wide range of Objects, particularly in the context of a [Process] that deleted other Objects.

### Inverse

[Created](#Created)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[File]|A process deleted a file during its execution.|
|[Process]|[Win Registry Key]|A process deleted a Windows registry key or registry key value during its execution.|
|[Process]|[Win Service]|A process deleted a Windows service during its execution.|
|[Process]|[Mutex]|A process deleted a mutex during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Deleted</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Deleted_By"></a> "Deleted_By"

The **source Object** was *Deleted by* the **related Object**. Applicable to a wide range of Objects, particularly in the
context of Objects that were deleted by a [Process].

### Inverse

[Created_By](#Created_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Process]|A file was deleted by a process during its execution.|
|[Win Registry Key]|[Process]|A Windows registry key or registry key value was deleted by a process during its execution.|
|[Win Service]|[Process]|A Windows service was deleted by a process during its execution.|
|[Mutex]|[Process]|A mutex was deleted by a process during its execution.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Deleted_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Modified_Properties_Of"></a> "Modified_Properties_Of"

The **source Object** *Modifed the properties of* the **related Object**. Applicable to a wide range of Objects, particularly in the
context of a [Process] that modified the properties of other Objects.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[File]|A process modified the properties of a file during its execution.|
|[Process]|[Win Registry Key]|A process modified the properties of a Windows registry key or registry key value during its execution.|
|[Process]|[Win Service]|A process modified the properties of a Windows service during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Modified_Properties_Of</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Properties_Modified_By"></a> "Properties_Modified_By"

The **source Object** had its *Properties modified* by the **related Object**. Applicable to a wide range of Objects, particularly in the context of Objects whose properties were modified by a [Process].

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Process]|A file had its properties modified by a process during its execution.|
|[Win Registry Key]|[Process]|A Windows registry key or registry key value had its properties modified by a process during its execution.|
|[Win Service]|[Process]|A Windows service had its properties modified by a process during its execution.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Properties_Modified_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Downloaded_From"></a> "Downloaded_From"

The **source Object** was *Downloaded from* the **related Object**. Commonly used for expressing the fact that a file was downloaded from some network location.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[URI]|A file was downloaded from some particular URL.|
|[File]|[Domain Name]|A file was downloaded from some particular domain name.|
|[File]|[Address]|A file was downloaded from some particular IP address.|
|[File]|[Hostname]|A file was downloaded from some device identified by a particular hostname.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-d9f7b338-a20f-47b2-9efd-21f5a42b54f1">
			<cybox:Properties xsi:type="DomainNameObj:DomainNameObjectType">
				<DomainNameObj:Value>example.com</DomainNameObj:Value>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Downloaded_From</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Downloaded"></a> "Downloaded"

The **source Object** *Downloaded* the **related Object**. Commonly used for expressing the fact that a process downloaded a file.

### Inverse

[Uploaded](#Uploaded)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[File]|A process downloaded a particular file during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Downloaded</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Downloaded_To"></a> "Downloaded_To"

The **source Object** was *Downloaded to* the **related Object**. Commonly used for expressing the fact that a file or URL that refers to a file was downloaded as another file (e.g., "abcd.exe" downloaded as "fun.jpg") or to a particular location.

### Inverse

[Uploaded_To](#Uploaded_To)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[URI]|[File]|A file specified by a URL was downloaded and stored as another file or at some particular location.|
|[File]|[File]|A file was downloaded and stored as another file or at some particular location.|

### Example

```xml
<cybox:Object id="example:object-51b8828d-3068-4a6d-96e9-7b19d3b3ef1a">
	<cybox:Properties xsi:type="URIObj:URIObjectType" type="URL">
		<URIObj:Value>http://example.com/asdfg.jpg</URIObj:Value>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-31a600e7-7357-4845-9604-70327c9a7dfc">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>/usr/tmp/test.bin</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Downloaded_To</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Downloaded_By"></a> "Downloaded_By"

The **source Object** was *Downloaded by* the **related Object**. Commonly used for expressing the fact that a file was downloaded by a process.

### Inverse

[Uploaded_By](#Uploaded_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Process]|A file was downloaded by a particular process during its execution.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Downloaded_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Uploaded"></a> "Uploaded"

The **source Object** *Uploaded* the **related Object**. Commonly used for expressing the fact that a process uploaded a particular file.

### Inverse

[Downloaded](#Downloaded)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[File]|A process uploaded a particular file during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Uploaded</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Uploaded_By"></a> "Uploaded_By"

The **source Object** was *Uploaded by* the **related Object**. Commonly used for expressing the fact that a file was uploaded by a process.

### Inverse

[Downloaded_By](#Downloaded_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Process]|A file was uploaded by a particular process during its execution.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Uploaded_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Uploaded_To"></a> "Uploaded_To"

The **source Object** was *Uploaded to* the **related Object**. Commonly used for expressing the fact that a file was uploaded to a particular network location.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[URI]|A file was uploaded to a particular URL.|
|[File]|[Domain Name]|A file was uploaded to a particular domain name.|
|[File]|[Address]|A file was uploaded to a particular IP address.|
|[File]|[Hostname]|A file was uploaded to a device identified by a particular hostname.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-0eaf497e-1062-4d52-97fa-670c4426ff3b">
			<cybox:Properties xsi:type="AddressObj:AddressObjectType" category="ipv4-addr">
				<AddressObj:Address_Value>10.1.2.3</AddressObj:Address_Value>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Uploaded_To</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Sent_To"></a> "Sent_To"

The **source Object** was *Sent to* the **related Object**. Commonly used for expressing the fact that a file was sent to a particular email address.

### Inverse

[Received_From](#Received_From)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Address]|A file was sent to a particular email address.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-54710212-ca56-4eb6-8b4a-f8bf083303ae">
			<cybox:Properties xsi:type="AddressObj:AddressObjectType" category="e-mail">
				<AddressObj:Address_Value>bob@example.com</AddressObj:Address_Value>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Sent_To</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Received_From"></a> "Received_From"

The **source Object** was *Received from* the **related Object**. Commonly used for expressing the fact that a file was received from an email sent from a particular email address.

### Inverse

[Sent_To](#Sent_To)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Address]|A file was received from an email sent from particular email address.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-238f4ee7-d986-4c6c-9e50-4474270582a2">
			<cybox:Properties xsi:type="AddressObj:AddressObjectType" category="e-mail">
				<AddressObj:Address_Value>sue@example.com</AddressObj:Address_Value>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Received_From</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Values_Enumerated"></a> "Values_Enumerated"

The **source Object** *Enumerated the values* of the **related Object**. Commonly used for expressing the fact that a process enumerated the values of a particular Windows registry key.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Win Registry Key]|A process enumerated the values of a particular Windows registry key during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-0eaf497e-1062-4d52-97fa-670c4426ff3b">
			<cybox:Properties xsi:type="WinRegistryKeyObj:WindowsRegistryKeyObjectType">
				<WinRegistryKeyObj:Key>System\services\ACPI</WinRegistryKeyObj:Key>
				<WinRegistryKeyObj:Hive>HKEY_LOCAL_MACHINE</WinRegistryKeyObj:Hive>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Values_Enumerated</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Values_Enumerated_By"></a> "Values_Enumerated_By"

The **source Object** had its *Values enumerated* by the **related Object**. Commonly used for expressing the fact that a Windows registry key had its values enumerated by a particular process.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Win Registry Key]|[Process]|A Windows registry key had its values enumerated by a particular process during its execution.|

### Example

```xml
<cybox:Object id="example:object-0eaf497e-1062-4d52-97fa-670c4426ff3b">
	<cybox:Properties xsi:type="WinRegistryKeyObj:WindowsRegistryKeyObjectType">
		<WinRegistryKeyObj:Key>System\services\ACPI</WinRegistryKeyObj:Key>
		<WinRegistryKeyObj:Hive>HKEY_LOCAL_MACHINE</WinRegistryKeyObj:Hive>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Values_Enumerated_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Killed"></a> "Killed"

The **source Object** *Killed* the **related Object**. Commonly used for expressing the fact that a process killed (or terminated) another process or thread.

### Inverse

[Killed](#Killed)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Process]|A process killed (or terminated) another process during its execution.|
|[Process]|[Win Thread]|A process killed (or terminated) a thread during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-b464a2a1-876b-4e29-9b5f-705f66ca1327">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>another_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Killed</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Killed_By"></a> "Killed_By"

The **source Object** was *Killed by* the **related Object**. Commonly used for expressing the fact that a process or thread was killed (or terminated) by another process.

### Inverse

[Created_By](#Created_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Process]|A process was killed (or terminated) by another process during its execution.|
|[Win Thread]|[Process]|A Windows thread was killed (or terminated) by a process during its execution.|

### Example

```xml
<cybox:Object id="example:object-b464a2a1-876b-4e29-9b5f-705f66ca1327">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>another_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Killed_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Locked"></a> "Locked"

The **source Object** *Locked* the **related Object**. Commonly used for expressing the fact that a process locked (in terms of read, write, or delete access) a particular file.

### Inverse

[Unlocked](#Unlocked)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[File]|A process locked (in terms of read, write, or delete access) a particular file during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Locked</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Locked_By"></a> "Locked_By"

The **source Object** was *Locked by* the **related Object**. Commonly used for expressing the fact that a file was locked (in terms of read, write, or delete access) by a particular process.

### Inverse

[Unlocked_By](#Unlocked_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Process]|A file was locked (in terms of read, write, or delete access) by a particular process during its execution.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Locked_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Unlocked"></a> "Unlocked"

The **source Object** *Unlocked* the **related Object**. Commonly used for expressing the fact that a process unlocked (in terms of read, write, or delete access) a particular file.

### Inverse

[Locked](#Locked)

### Applicable Objects
|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[File]|A process unlocked (in terms of read, write, or delete access) a particular file during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Unlocked</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Unlocked_By"></a> "Unlocked_By"

The **source Object** was *Unlocked by* the **related Object**. Commonly used for expressing the fact that a file was unlocked (in terms of read, write, or delete access) by a particular process.

### Inverse

[Locked_By](#Locked_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Process]|A file was unlocked (in terms of read, write, or delete access) by a particular process during its execution.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Unlocked_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Listened_On"></a> "Listened_On"

The **source Object** *Listened on* the **related Object**. Commonly used for expressing the fact that a process listened on a particular port or socket.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Port]|A process listened on a particular port during its execution.|
|[Process]|[Network Socket]|A process listened on a particular network socket during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-892a4b26-59af-4dcf-88f3-f55f3837fbde">
			<cybox:Properties xsi:type="PortObj:PortObjectType">
			  <PortObj:Port_Value>1234</PortObj:Port_Value>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Listened_On</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Renamed"></a> "Renamed"

The **source Object** *Renamed* the **related Object**. Commonly used for expressing the fact that a process renamed a particular file.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[File]|A process renamed a file during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Renamed</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Renamed_By"></a> "Renamed_By"

The **source Object** was *Renamed by* the **related Object**.  Commonly used for expressing the fact that a file was renamed by a particular process.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Process]|A file was renamed by a particular process during its execution.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Renamed_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Renamed_From"></a> "Renamed_From"

The **source Object** was *Renamed from* the **related Object**.  Commonly used for expressing the fact that a file was renamed from a version of the file with a different name.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[File]|A file was renamed from another version of the file with a different name.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-d64e3ee9-39bf-4149-ae77-9b2df9c203e3">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\asdfg.bin</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Renamed_From</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Renamed_To"></a> "Renamed_To"

The **source Object** was *Renamed to* the **related Object**.  Commonly used for expressing the fact that a file was renamed to a version of the file with a different name.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[File]|A file was renamed to another version of the file with a different name.|

### Example

```xml
<cybox:Object id="example:object-d64e3ee9-39bf-4149-ae77-9b2df9c203e3">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\asdfg.bin</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Renamed_To</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Moved"></a> "Moved"

The **source Object** *Moved* the **related Object**. Commonly used for expressing the fact that a process moved a particular file from one location to another.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[File]|A process moved a file during its execution, from one location to another.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Moved</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Moved_By"></a> "Moved_By"

The **source Object** was *Moved by* the **related Object**.  Commonly used for expressing the fact that a file was moved by a particular process, from one location to another.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Process]|A file was moved by a particular process during its execution, from one location to another.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Moved_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Moved_From"></a> "Moved_From"

The **source Object** was *Moved from* the **related Object**.  Commonly used for expressing the fact that a file was moved from one location to another.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[File]|A file was moved from one location to another (represented as a separate file).|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-d64e3ee9-39bf-4149-ae77-9b2df9c203e3">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\asdfg.bin</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Moved_From</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Moved_To"></a> "Moved_To"

The **source Object** was *Moved to* the **related Object**.  Commonly used for expressing the fact that a file was moved from one location to another.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[File]|A file was moved from one location to another (represented as a separate file).|

### Example

```xml
<cybox:Object id="example:object-d64e3ee9-39bf-4149-ae77-9b2df9c203e3">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\asdfg.bin</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Moved_To</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Copied"></a> "Copied"

The **source Object** *Copied* the **related Object**. Commonly used for expressing the fact that a process copied a particular file from one location to another.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[File]|A process copied a file during its execution, from one location to another.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Copied</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Copied_By"></a> "Copied_By"

The **source Object** was *Copied by* the **related Object**.  Commonly used for expressing the fact that a file was copied by a particular process, from one location to another.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Process]|A file was copied by a particular process during its execution, from one location to another.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Copied_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Copied_From"></a> "Copied_From"

The **source Object** was *Copied from* the **related Object**.  Commonly used for expressing the fact that a file was copied from one location to another.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[File]|A file was copied from one location to another (represented as a separate file).|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-d64e3ee9-39bf-4149-ae77-9b2df9c203e3">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\asdfg.bin</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Copied_From</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Copied_To"></a> "Copied_To"

The **source Object** was *Copied to* the **related Object**.  Commonly used for expressing the fact that a file was copied to one location from another.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[File]|A file was copied to one location from another (represented as a separate file).|

### Example

```xml
<cybox:Object id="example:object-d64e3ee9-39bf-4149-ae77-9b2df9c203e3">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\asdfg.bin</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Copied_To</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Contains"></a> "Contains"

The **source Object** *Contains* the **related Object**.  Used for expressing the fact that an object contains another object inside of it. 

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[File]|A file contains another file inside of it (e.g. appended to it).|
|[Archive File]|[File]|An archive file contains another file inside of it.|
|[Email Message]|[File]|An email message contains a file as an attachment.|
|[Email Message]|[Link]|An email message contains a link within its message body.|
|[URI]|[Domain Name]|A URL contains a domain name as part of its structure.|
|[DNS Record]|[Address]|A DNS record contains an IP address that resolves to the domain identified by the record.|
|[ARP Cache]|[Address]|An ARP cache contains a physical (i.e. MAC) address or IP address in one of its entries.|
|[URL History]|[URI]|A URL history cache contains a particular URL in one of its entries.|
|[Win Registry Key]|[Win Registry Key]|A Windows registry key contains another Windows registry key, as a subkey.|

### Example

```xml
<cybox:Object id="example:object-210ff682-5362-4391-be79-dfa60f947c07">
	<cybox:Properties xsi:type="ArchiveFileObj:ArchiveFileObjectType">
		<FileObj:File_Path>archive.zip</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-a4a74a15-e2ae-4df2-ab4e-c24cf4178fe9">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>README.txt</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Contains</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Contained_Within"></a> "Contained_Within"

The **source Object** is *Contained within* the **related Object**.  Used for expressing the fact that an object is contained within another object. 

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[File]|A file is contained within another file (e.g. appended to it).|
|[File]|[Archive File]|A file is contained within an archive file.|
|[File]|[Email Message]|A file is contained within an email message, as an attachment.|
|[Link]|[Email Message]|A link is contained within the body of an email message.|
|[Domain Name]|[URI]|A domain name is contained within the structure of a URL.|
|[Address]|[DNS Record]|A IP address is contained within a DNS record that resolves to the domain identified by the record.|
|[Address]|[ARP Cache]|A physical (i.e. MAC) address or IP address is contained within one of the entries of an ARP cache.|
|[URI]|[URL History]|A URL is contained within one of the entries of a URL history cache.|
|[Win Registry Key]|[Win Registry Key]|A Windows registry key is contained within another Windows registry key, as a subkey.|

### Example

```xml
<cybox:Object id="example:object-a4a74a15-e2ae-4df2-ab4e-c24cf4178fe9">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>README.txt</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-210ff682-5362-4391-be79-dfa60f947c07">
			<cybox:Properties xsi:type="ArchiveFileObj:ArchiveFileObjectType">
				<FileObj:File_Path>archive.zip</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Contained_Within</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Extracted_From"></a> "Extracted_From"

The **source Object** was *Extracted from* the **related Object**.  Used for expressing the fact that an object was extracted from another object, in the sense that the extracted object was physically encapsulated in the structure of the object that it was extracted from, as in a file extracted from an archive file.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[File]|A file was extracted from inside of another file.|
|[File]|[Archive File]|A file was extracted from an archive file.|
|[URI]|[Email Message]|A URL was extracted from the body of an email message.|
|[Link]|[Email Message]|A link was extracted from the body of an email message.|

### Example

```xml
<cybox:Object id="example:object-210ff682-5362-4391-be79-dfa60f947c07">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\README.txt</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-210ff682-5362-4391-be79-dfa60f947c07">
			<cybox:Properties xsi:type="ArchiveFileObj:ArchiveFileObjectType">
				<FileObj:File_Path>archive.zip</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Extracted_From</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Connected_To"></a> "Connected_To"

The **source Object** *Connected to* the **related Object**.  Commonly used for expressing the fact that a process connected to some network location or resource.

### Inverse

n/a

### Applicable Objects
|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Address]|A process connected to an IP address.|
|[Process]|[Hostname]|A process connected to a hostname.|
|[Process]|[Socket Address]|A process connected to a socket address.|
|[Process]|[Network Socket]|A process connected to a network socket.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-dec3774a-ee00-4fe8-9a19-924d51f7a46a">
			<cybox:Properties xsi:type="AddressObj:AddressObjectType" category="ipv4-addr">
				<AddressObj:Address_Value>10.1.2.5</AddressObj:Address_Value>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Connected_To</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Parent_Of"></a> "Parent_Of"

The **source Object** is the *Parent of* the **related Object**.  Commonly used for expressing the fact that a process spawned another process or thread and is therefore its parent.

### Inverse

[Child_Of](#Child_Of)

### Applicable Objects
|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Process]|A process is the parent of another process (which it spawned).|
|[Process]|[Win Thread]|A process is the parent of a Windows thread (which it spawned).|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-b464a2a1-876b-4e29-9b5f-705f66ca1327">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>another_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Parent_Of</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Child_Of"></a> "Child_Of"

The **source Object** is a *Child of* the **related Object**.  Commonly used for expressing the fact that a process or thread was spawned by another process and is therefore its child.

### Inverse

[Parent_Of](#Parent_Of)

### Applicable Objects
|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Process]|A process is the child of another process (which spawned it).|
|[Win Thread]|[Process]|A Windows thread is the child of a process (which spawned it).|

### Example

```xml 
<cybox:Object id="example:object-b464a2a1-876b-4e29-9b5f-705f66ca1327">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>another_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Child_Of</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Redirects_To"></a> "Redirects_To"

The **source Object** *Redirects to* the **related Object**.  Commonly used for expressing URL or domain name redirection, where a URL redirects to another URL, or a [Domain Name] redirects to another [Domain Name], respectively.

### Inverse

n/a

### Applicable Objects
|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[URI]|[URI]|A URL redirects to another URL.|
|[Domain Name]|[Domain Name]|A domain name redirects to another domain name.|

### Examples

```xml 
<cybox:Object id="example:object-ee973e87-6811-4bb0-aba2-59ffbd6e110d">
	<cybox:Properties xsi:type="URIObj:URIObjectType">
		<URIObj:Value>http://example.com/redir</URIObj:Value>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-ac8fd3b0-ad06-4c66-8cc9-39581e2c0564">
			<cybox:Properties xsi:type="URIObj:URIObjectType">
				<URIObj:Value>http://example.net/another_page</URIObj:Value>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Redirects_To</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Suspended"></a> "Suspended"

The **source Object** *Suspended* the **related Object**. Commonly used for expressing the fact that a process suspended the execution of another process or thread.

### Inverse

[Resumed](#Resumed)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Process]|A process suspended the execution of another process.|
|[Process]|[Win Thread]|A process suspended the execution of a Windows thread.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-b464a2a1-876b-4e29-9b5f-705f66ca1327">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>another_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Suspended</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Suspended_By"></a> "Suspended_By"

The **source Object** was *Suspended by* the **related Object**. Commonly used for expressing the fact that the execution of a process or thread was suspended by another process.

### Inverse

[Resumed_By](#Resumed_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Process]|A process was suspended by another process.|
|[Win Thread]|[Process]|A Windows thread was suspended by a process.|

### Example

```xml
<cybox:Object id="example:object-b464a2a1-876b-4e29-9b5f-705f66ca1327">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>another_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Suspended_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Paused"></a> "Paused"

The **source Object** *Paused* the **related Object**. Commonly used for expressing the fact that a process paused the execution of a Windows service.

### Inverse

[Resumed](#Resumed)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Win Service]|A process paused the execution of a Windows service.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-355010b4-33de-4627-92d7-9a634dea668d">
			<cybox:Properties xsi:type="WinServiceObj:WindowsServiceObjectType">
				<WinServiceObj:Display_Name>boot svc</WinServiceObj:Display_Name>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Paused</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Paused_By"></a> "Paused_By"

The **source Object** was *Paused by* the **related Object**. Commonly used for expressing the fact that the execution of a Windows service was paused by a process.

### Inverse

[Resumed_By](#Resumed_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Win Service]|[Process]|A Windows service was paused by a process.|

### Example

```xml
<cybox:Object id="example:object-355010b4-33de-4627-92d7-9a634dea668d">
	<cybox:Properties xsi:type="WinServiceObj:WindowsServiceObjectType">
		<WinServiceObj:Display_Name>boot svc</WinServiceObj:Display_Name>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Paused_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Resumed"></a> "Resumed"

The **source Object** *Resumed* the **related Object**. Commonly used for expressing the fact that a process resumed the execution of another process, thread, or Windows service.

### Inverse

[Suspended](#Suspended)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Process]|A process resumed the execution of another process.|
|[Process]|[Win Thread]|A process resumed the execution of a Windows thread.|
|[Process]|[Win Service]|A process resumed the execution of a Windows service.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-b464a2a1-876b-4e29-9b5f-705f66ca1327">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>another_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Resumed</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Resumed_By"></a> "Resumed_By"

The **source Object** was *Resumed by* the **related Object**. Commonly used for expressing the fact that the execution of a process, thread, or Windows service was resumed by another process.

### Inverse

[Suspended_By](#Suspended_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Process]|A process was resumed by another process.|
|[Win Thread]|[Process]|A Windows thread was resumed by a process.|
|[Win Service]|[Process]|A Windows service was resumed by a process.|

### Example

```xml
<cybox:Object id="example:object-b464a2a1-876b-4e29-9b5f-705f66ca1327">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>another_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Resumed_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Wrote_To"></a> "Wrote_To"

The **source Object** *Wrote to* the **related Object**. Commonly used for expressing the fact that a process wrote to another object during its execution.

### Inverse

[Read_From](#Read_From)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Process]|A process wrote to the memory space of another process during its execution.|
|[Process]|[File]|A process wrote to a file during its execution.|
|[Process]|[Pipe]|A process wrote to a pipe during its execution.|
|[Process]|[Win Mailslot]|A process wrote to a Windows mailslot during its execution.|

### Example

```xml
<cybox:Object id="example:object-b464a2a1-876b-4e29-9b5f-705f66ca1327">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>another_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Wrote_To</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Written_To_By"></a> "Written_To_By"

The **source Object** was *Written to by* the **related Object**. Commonly used for expressing the fact that an object was written to by a process during its execution.

### Inverse

[Read_From_By](#Read_From_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Process]|The memory space of a process was written to by another process during its execution.|
|[File]|[Process]|A file was written to by a process during its execution.|
|[Pipe]|[Process]|A pipe was written to by a process during its execution.|
|[Win Mailslot]|[Process]|A Windows mailslot was written to by a process during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-b464a2a1-876b-4e29-9b5f-705f66ca1327">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>another_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Written_To_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Read_From"></a> "Read_From"

The **source Object** *Read from* the **related Object**. Commonly used for expressing the fact that a process read from another object during its execution.

### Inverse

[Wrote_To](#Wrote_To)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Process]|A process read from the memory space of another process during its execution.|
|[Process]|[File]|A process read from a file during its execution.|
|[Process]|[Pipe]|A process read from a pipe during its execution.|
|[Process]|[Win Mailslot]|A process read from a Windows mailslot during its execution.|

### Example

```xml
<cybox:Object id="example:object-b464a2a1-876b-4e29-9b5f-705f66ca1327">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>another_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Read_From</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Read_From_By"></a> "Read_From_By"

The **source Object** was *Read from by* the **related Object**. Commonly used for expressing the fact that an object was read from by a process during its execution.

### Inverse

[Written_To_By](#Written_To_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Process]|The memory space of a process was read from by another process during its execution.|
|[File]|[Process]|A file was read from by a process during its execution.|
|[Pipe]|[Process]|A pipe was read from by a process during its execution.|
|[Win Mailslot]|[Process]|A Windows mailslot was read from by a process during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-b464a2a1-876b-4e29-9b5f-705f66ca1327">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>another_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Read_From_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Allocated"></a> "Allocated"

The **source Object** *Allocated* the **related Object**. Commonly used for expressing the fact that a process allocated a particular memory region.

### Inverse

[Freed](#Freed)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Memory]|A process allocated a particular memory region.|
|[Process]|[Win Memory Page Region]|A process allocated a particular Windows memory page region.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-21dd8e8b-8608-46a6-aafc-87e3452fd836">
			<cybox:Properties xsi:type="MemoryObj:MemoryObjectType">
				<MemoryObj:Region_Size>192000</MemoryObj:Region_Size>
				<MemoryObj:Region_Start_Address>2F3CD1FF</MemoryObj:Region_Start_Address>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Allocated</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Allocated_By"></a> "Allocated_By"

The **source Object** was *Allocated by* the **related Object**. Commonly used for expressing the fact that a memory region was allocated by a particular process.

### Inverse

[Freed_By](#Freed_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Memory]|[Process]|A memory region was allocated by a particular process during its execution.|
|[Win Memory Page Region]|[Process]|A Windows memory page region was allocated by a particular process during its execution.|

### Example

```xml
<cybox:Object id="example:object-21dd8e8b-8608-46a6-aafc-87e3452fd836">
	<cybox:Properties xsi:type="MemoryObj:MemoryObjectType">
		<MemoryObj:Region_Size>192000</MemoryObj:Region_Size>
		<MemoryObj:Region_Start_Address>2F3CD1FF</MemoryObj:Region_Start_Address>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Allocated_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Freed"></a> "Freed"

The **source Object** *Freed* the **related Object**. Commonly used for expressing the fact that a process freed a particular memory region.

### Inverse

[Allocated](#Allocated)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[Memory]|A process freed a particular memory region.|
|[Process]|[Win Memory Page Region]|A process freed a particular Windows memory page region.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-21dd8e8b-8608-46a6-aafc-87e3452fd836">
			<cybox:Properties xsi:type="MemoryObj:MemoryObjectType">
				<MemoryObj:Region_Size>192000</MemoryObj:Region_Size>
				<MemoryObj:Region_Start_Address>2F3CD1FF</MemoryObj:Region_Start_Address>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Freed</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Freed_By"></a> "Freed_By"

The **source Object** was *Freed by* the **related Object**. Commonly used for expressing the fact that a memory region was freed by a particular process.

### Inverse

[Allocated_By](#Allocated_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Memory]|[Process]|A memory region was freed by a particular process during its execution.|
|[Win Memory Page Region]|[Process]|A Windows memory page region was freed by a particular process during its execution.|

### Example

```xml
<cybox:Object id="example:object-21dd8e8b-8608-46a6-aafc-87e3452fd836">
	<cybox:Properties xsi:type="MemoryObj:MemoryObjectType">
		<MemoryObj:Region_Size>192000</MemoryObj:Region_Size>
		<MemoryObj:Region_Start_Address>2F3CD1FF</MemoryObj:Region_Start_Address>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Freed_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Opened"></a> "Opened"

The **source Object** *Opened* the **related Object**. Commonly used for expressing the fact that a process opened an object for access, use, or modification.

### Inverse

[Closed](#Closed)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[File]|A process opened an existing file during its execution.|
|[Process]|[Win Filemapping]|A process opened an existing Windows filemapping during its execution.|
|[Process]|[Mutex]|A process opened an existing mutex during its execution.|
|[Process]|[Semaphore]|A process opened an existing semaphore during its execution.|
|[Process]|[Port]|A process opened a port during its execution.|
|[Process]|[Win Event]|A process opened an existing Windows event during its execution.|
|[Process]|[Win Critical Section]|A process opened an existing Windows critical section during its execution.|
|[Process]|[Win Handle]|A process opened an existing Windows handle during its execution.|
|[Process]|[Win Registry Key]|A process opened an existing Windows registry key during its execution.|
|[Process]|[Win Service]|A process opened an existing Windows service during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-a127818e-eb90-4290-ae7b-2fd1bf0801b0">
			<cybox:Properties xsi:type="MutexObj:MutexObjectType">
				<MutexObj:Name>some.mutex!</MutexObj:Name>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Opened</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Opened_By"></a> "Opened_By"

The **source Object** was *Opened_By* the **related Object**. Commonly used for expressing the fact that an object was opened by a process for access or modification.

### Inverse

[Closed_By](#Closed_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Process]|An existing file was opened by a particular process during its execution.|
|[Win Filemapping]|[Process]|An existing Windows filemapping was opened by a particular process during its execution.|
|[Mutex]|[Process]|An existing mutex was opened by a particular process during its execution.|
|[Port]|[Process]|A port was opened by a particular process during its execution.|
|[Semaphore]|[Process]|An existing semaphore was opened by a particular process during its execution.|
|[Win Event]|[Process]|An existing Windows event was opened by a particular process during its execution.|
|[Win Critical Section]|[Process]|An existing Windows critical section was opened by a particular process during its execution.|
|[Win Handle]|[Process]|An existing Windows handle was opened by a particular process during its execution.|
|[Win Registry Key]|[Process]|An existing Windows registry key was opened by a particular process during its execution.|
|[Win Service]|[Process]|An existing Windows service was opened by a particular process during its execution.|

### Example

```xml 
<cybox:Object id="example:object-a127818e-eb90-4290-ae7b-2fd1bf0801b0">
	<cybox:Properties xsi:type="MutexObj:MutexObjectType">
		<MutexObj:Name>some.mutex!</MutexObj:Name>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Opened_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Closed"></a> "Closed"

The **source Object** *Closed* the **related Object**. Commonly used for expressing the fact that a process closed an object that was previously opened for access, use, or modification.

### Inverse

[Opened](#Opened)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Process]|[File]|A process closed an existing file during its execution.|
|[Process]|[Win Filemapping]|A process closed an existing Windows filemapping during its execution.|
|[Process]|[Port]|A process closed a port during its execution.|
|[Process]|[Win Handle]|A process closed an existing Windows handle during its execution.|
|[Process]|[Win Registry Key]|A process closed an existing Windows service during its execution.|

### Example

```xml
<cybox:Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
	<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
		<ProcessObj:Image_Info>
			<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
		</ProcessObj:Image_Info>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-265b2078-1b32-4c1e-aa49-d8a5162ee9f9">
			<cybox:Properties xsi:type="PortObj:PortObjectType">
				<PortObj:Port_Value>222</PortObj:Port_Value>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Closed</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Closed_By"></a> "Closed_By"

The **source Object** was *Closed_By* the **related Object**. Commonly used for expressing the fact that an object previously opened for access or modification was closed by a process.

### Inverse

[Opened_By](#Opened_By)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Process]|An existing file was closed by a particular process during its execution.|
|[Win Filemapping]|[Process]|An existing Windows filemapping was closed by a particular process during its execution.|
|[Port]|[Process]|A port was closed by a particular process during its execution.|
|[Win Handle]|[Process]|An existing Windows handle was closed by a particular process during its execution.|
|[Win Registry Key]|[Process]|An existing Windows registry key was closed by a particular process during its execution.|

### Example

```xml 
<cybox:Object id="example:object-265b2078-1b32-4c1e-aa49-d8a5162ee9f9">
	<cybox:Properties xsi:type="PortObj:PortObjectType">
		<PortObj:Port_Value>222</PortObj:Port_Value>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-c822a70d-7b41-4553-983b-a07fd8c553a0">
			<cybox:Properties xsi:type="ProcessObj:ProcessObjectType">
				<ProcessObj:Image_Info>
					<ProcessObj:File_Name>some_process.exe</ProcessObj:File_Name>
				</ProcessObj:Image_Info>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Closed_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```

---

## <a name="Characterizes"></a> "Characterizes"

The **source Object** *Characterizes* the **related Object**.  Used for expressing the fact that an object characterizes or provides information on the features of another object.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[Artifact]|A file defines the file-specific features that characterize an artifact.|
|[DNS Record]|[Domain Name]|A DNS record defines the DNS-record-specific features that characterize a domain name.|
|[WHOIS]|[Domain Name]|A WHOIS record defines the WHOIS-specific features that characterize a domain name.|


### Example

```xml 
<cybox:Object id="example:object-2efb4279-86e6-4554-a8e0-8d6d2610e632">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Name>asdfg.dll</FileObj:File_Name>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-dfd1d908-a799-4d9b-b367-63c556979a89">
			<cybox:Properties xsi:type="ArtifactObj:ArtifactObjectType">
				<ArtifactObj:Raw_Artifact>ABCDFFFF</ArtifactObj:Raw_Artifact>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Characterizes</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>							
</cybox:Object>
```

---

## <a name="Characterized_By"></a> "Characterized_By"

The **source Object** is *Characterized by* the **related Object**.  Used for expressing the fact that an object is characterized by another object, which provides information on its features.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Artifact]|[File]|An artifact is characterized by a file, which defines its file-specific features.|
|[Domain Name]|[DNS Record]|A domain name is characterized by a DNS record, which defines its DNS-record-specific features.|
|[Domain Name]|[WHOIS]|A domain name is characterized by a WHOIS record, which defines its WHOIS-specific features.|


### Example

```xml
<cybox:Object id="example:object-dfd1d908-a799-4d9b-b367-63c556979a89">
	<cybox:Properties xsi:type="ArtifactObj:ArtifactObjectType">
		<ArtifactObj:Raw_Artifact>ABCDFFFF</ArtifactObj:Raw_Artifact>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-2efb4279-86e6-4554-a8e0-8d6d2610e632">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Name>asdfg.dll</FileObj:File_Name>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Characterized_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>							
</cybox:Object>
```

---

## <a name="Resolved_To"></a> "Resolved_To"

The **source Object** *Resolved to* the **related Object**.  Used for expressing resolution between network naming structures (e.g. domain names) and IP addresses, in either direction.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Domain Name]|[Address]|A domain name resolved to a particular IP address.|
|[Hostname]|[Address]|A hostname resolved to a particular IP address.|
|[Address]|[Domain Name]|An IP address resolved to a particular domain name.|
|[Address]|[Hostname]|An IP address resolved to a particular hostname.|

### Example

```xml 
<cybox:Object id="example:object-711f7c33-e7b7-4843-aec7-2b0cdb7d132d">
	<cybox:Properties xsi:type="DomainNameObj:DomainNameObjectType">
		<DomainNameObj:Value>example.com</DomainNameObj:Value>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-10953c1c-c077-4db5-a35e-38094ac004c2">
			<cybox:Properties xsi:type="AddressObj:AddressObjectType">
				<AddressObj:Address_Value>1.2.3.4</AddressObj:Address_Value>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Resolved_To</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>							
</cybox:Object>
```

---

## <a name="Sub-domain_Of"></a> "Sub-domain_Of"

The **source Object** is a *Sub-domain* of the **related Object**.  Used for expressing the fact that a domain is a sub-domain of another domain.

### Inverse

[Supra-domain_Of](#Supra-domain_Of)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Domain Name]|[Domain Name]|A domain name is a sub-domain of another domain name.|

### Example

```xml 
<cybox:Object id="example:object-5d0268ae-3ddb-4eb4-b279-5f4b9f3800b6">
	<cybox:Properties xsi:type="DomainNameObj:DomainNameObjectType">
		<DomainNameObj:Value>test.example.com</DomainNameObj:Value>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-711f7c33-e7b7-4843-aec7-2b0cdb7d132d">
			<cybox:Properties xsi:type="DomainNameObj:DomainNameObjectType">
				<DomainNameObj:Value>example.com</DomainNameObj:Value>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Sub-domain_Of</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>							
</cybox:Object>
```

---

## <a name="Supra-domain_Of"></a> "Supra-domain_Of"

The **source Object** is a *Supra-domain* of the **related Object**.  Used for expressing the fact that a domain is a supra-domain of another domain.

### Inverse

[Sub-domain_Of](#Sub-domain_Of)

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Domain Name]|[Domain Name]|A domain name is a supra-domain of another domain name.|

### Example

```xml 
<cybox:Object id="example:object-711f7c33-e7b7-4843-aec7-2b0cdb7d132d">
	<cybox:Properties xsi:type="DomainNameObj:DomainNameObjectType">
		<DomainNameObj:Value>example.com</DomainNameObj:Value>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-5d0268ae-3ddb-4eb4-b279-5f4b9f3800b6">
			<cybox:Properties xsi:type="DomainNameObj:DomainNameObjectType">
				<DomainNameObj:Value>test.example.com</DomainNameObj:Value>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Supra-domain_Of</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>							
</cybox:Object>
```

---

## <a name="FQDN_Of"></a> "FQDN_Of"

The **source Object** is the *Fully-qualified domain name* of the **related Object**.  Used for expressing the fact that a domain name represents a fully-qualified domain name for a domain or hostname.

### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[Domain Name]|[Domain Name]|A domain name is a fully-qualified domain name for another domain name.|
|[Domain Name]|[Hostname]|A domain name is a fully-qualified domain name for a hostname.|

### Example

```xml 
<cybox:Object id="example:object-375ee123-277e-4f2d-ac7a-5d0ab823d1d1">
	<cybox:Properties xsi:type="DomainNameObj:DomainNameObjectType">
		<DomainNameObj:Value>www.example.com</DomainNameObj:Value>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-711f7c33-e7b7-4843-aec7-2b0cdb7d132d">
			<cybox:Properties xsi:type="DomainNameObj:DomainNameObjectType">
				<DomainNameObj:Value>example.com</DomainNameObj:Value>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">FQDN_Of</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>							
</cybox:Object>
```

---

## <a name="Dropped"></a> "Dropped"

The **source Object** *Dropped* the **related Object**.  Commonly used for expressing the fact that a file dropped another file, in the sense that the file, after being injected into or spawned as a process, created the other file.
 
### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[File]|A file dropped another file.|

### Example

```xml
<cybox:Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-2c6a7384-e9bd-457c-84ed-44a4e9d9048c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\asdfg.bin</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Dropped</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

## <a name="Dropped_By"></a> "Dropped_By"

The **source Object** was *Dropped by* the **related Object**.  Commonly used for expressing the fact that a file was dropped by another file, in the sense that it was created by the other file after it was injected or spawned as a process.
 
### Inverse

n/a

### Applicable Objects

|Source Object|Related Object|Description|
|-------------|--------------|-----------|
|[File]|[File]|A file was dropped by another file.|

### Example

```xml 
<cybox:Object id="example:object-2c6a7384-e9bd-457c-84ed-44a4e9d9048c">
	<cybox:Properties xsi:type="FileObj:FileObjectType">
		<FileObj:File_Path>C:\asdfg.bin</FileObj:File_Path>
	</cybox:Properties>
	<cybox:Related_Objects>
		<cybox:Related_Object id="example:object-e970c3df-0c01-4611-8257-6b01d188983c">
			<cybox:Properties xsi:type="FileObj:FileObjectType">
				<FileObj:File_Path>C:\temp\qwerty.dll</FileObj:File_Path>
			</cybox:Properties>
			<cybox:Relationship xsi:type="cyboxVocabs:ObjectRelationshipVocab-1.1">Dropped_By</cybox:Relationship>
		</cybox:Related_Object>
	</cybox:Related_Objects>
</cybox:Object>
```	

---

[Address]: http://stixproject.github.io/data-model/1.1.1/AddressObj/AddressObjectType/
[Archive File]: http://stixproject.github.io/data-model/1.1.1/ArchiveFileObj/ArchiveFileObjectType/
[Artifact]: http://stixproject.github.io/data-model/1.1.1/ArtifactObj/ArtifactObjectType/
[ARP Cache]: http://stixproject.github.io/data-model/1.1.1/ARPCacheObj/ARPCacheObjectType/
[Domain Name]: http://stixproject.github.io/data-model/1.1.1/DomainNameObj/DomainNameObjectType/
[DNS Record]: http://stixproject.github.io/data-model/1.1.1/DNSRecordObj/DNSRecordObjectType/
[Email Message]: http://stixproject.github.io/data-model/1.1.1/EmailMessageObj/EmailMessageObjectType/
[File]: http://stixproject.github.io/data-model/1.1.1/FileObj/FileObjectType/
[Hostname]: http://stixproject.github.io/data-model/1.1.1/HostnameObj/HostnameObjectType/
[Link]: http://stixproject.github.io/data-model/1.1.1/LinkObj/LinkObjectType/
[Memory]: http://stixproject.github.io/data-model/1.1.1/MemoryObj/MemoryObjectType/
[Mutex]: http://stixproject.github.io/data-model/1.1.1/MutexObj/MutexObjectType/
[Network Socket]: http://stixproject.github.io/data-model/1.1.1/NetworkSocketObj/NetworkSocketObjectType/
[Pipe]: http://stixproject.github.io/data-model/1.1.1/PipeObj/PipeObjectType/
[Port]: http://stixproject.github.io/data-model/1.1.1/PortObj/PortObjectType/
[Process]: http://stixproject.github.io/data-model/1.1.1/ProcessObj/ProcessObjectType/
[Semaphore]: http://stixproject.github.io/data-model/1.1.1/SemaphoreObj/SemaphoreObjectType/
[Socket Address]: http://stixproject.github.io/data-model/1.1.1/SocketAddressObj/SocketAddressObjectType/
[URI]: http://stixproject.github.io/data-model/1.1.1/URIObj/URIObjectType/
[URL History]: http://stixproject.github.io/data-model/1.1.1/URLHistoryObj/URLHistoryObjectType/
[Win Critical Section]: http://stixproject.github.io/data-model/1.1.1/WinCriticalSectionObj/WindowsCriticalSectionObjectType/
[Win Event]: http://stixproject.github.io/data-model/1.1.1/WinEventObj/WindowsEventObjectType/
[Win Filemapping]: http://stixproject.github.io/data-model/1.1.1/WinFilemappingObj/WindowsFilemappingObjectType/
[Win Handle]: http://stixproject.github.io/data-model/1.1.1/WinHandleObj/WindowsHandleObjectType/
[Win Registry Key]: http://stixproject.github.io/data-model/1.1.1/WinRegistryKeyObj/WindowsRegistryKeyObjectType/
[Win Service]: http://stixproject.github.io/data-model/1.1.1/WinServiceObj/WindowsServiceObjectType/
[Win Thread]: http://stixproject.github.io/data-model/1.1.1/WinThreadObj/WindowsThreadObjectType/
[Win Mailslot]: http://stixproject.github.io/data-model/1.1.1/WinMailslotObj/WindowsMailslotObjectType/
[Win Memory Page Region]: http://stixproject.github.io/data-model/1.1.1/WinMemoryPageRegionObj/WindowsMemoryPageRegionObjectType/
[WHOIS]: http://stixproject.github.io/data-model/1.1.1/WhoisObj/WhoisObjectType/
