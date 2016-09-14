.. deleting_expeditions

Deleting expedtions
===============
With an on delete cascade its easy to delete bad expeditions just by deleting a single expedition from the expeditions table:

Here is the table syntax:
ALTER TABLE `expeditionBcids` ADD FOREIGN KEY (`expeditionId`) REFERENCES `expeditions` (`expeditionId`) ON DELETE CASCADE;

An example for deletion becomes:

delete from expeditions where expeditionId = 873;


