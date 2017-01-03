FIMS v1 migration to FIMS v2
============================

Instructions for updating deployment for nmnh-fims and biscicol-fims. 

Run the FimsAlterTableScript in biocode-fims-commons.

To use the FimsAlterTablesScript:

1. copy and paste the "mysql --batch --skip-column-names ..." to the cmd line.
2. copy the output
3. enter the mysql prompt
4. paste the output.
5. copy and paste the "drop table" and "alter table" lines from the FimsAlterTableScript to the mysql prompt. I recommend doing this in blocks and not just copy and pasting everything at once.

After you complete the db migration, run the biocode.fims.utils.ExpeditionUpdater "main" method in biocode-fims-commons. This will create bcids for all of the expeditions.
