



https://b0uh.github.io/django-model-change-field-name-with-no-db-impact.html



makemigrations <app-name> is only needed when migration folder specific to app and inside the app folder is empty, thus, a new migration document needs to be initaed.

https://stackoverflow.com/questions/36153748/django-makemigrations-no-changes-detected



`makemigrations -v 3`  for verbosity


## Special case 
Model name was old and has changed but migration added the `RenameModel` somewhere below the `Update field`, thus, error. 

the error was 

```bash
KeyError: ('respi', 'microcatchment_establishment')
```

old migration definition

```sql
respi_microcatchment;
                                               Table "public.respi_microcatchment"
           Column           |           Type           | Collation | Nullable |                     Default
----------------------------+--------------------------+-----------+----------+--------------------------------------------------
 id                         | integer                  |           | not null | nextval('respi_microcatchment_id_seq'::regclass)
 recorded_dte               | timestamp with time zone |           | not null |
 microcatchment_type        | character varying(50)    |           | not null |
 total_microcatchments      | integer                  |           | not null |
 established_date           | date                     |           | not null |
 length                     | double precision         |           | not null |
 width                      | double precision         |           | not null |
 depth                      | double precision         |           | not null |
 vertical_spacing           | double precision         |           | not null |
 horizontal_spacing         | double precision         |           | not null |
 reseeded                   | boolean                  |           | not null |
 quantity_seeds_sown        | integer                  |           |          |
 sow_unit                   | character varying(10)    |           |          |
 seed_sources               | character varying(255)   |           | not null |
 local_seed_bank_name       | character varying(50)    |           |          |
 other_seed_sources         | character varying(100)   |           |          |
 who_manages_microcatchment | character varying(255)   |           | not null |
 other_managements_gender   | character varying(100)   |           |          |
 management_practices       | character varying(255)   |           | not null |
 other_managements          | character varying(100)   |           |          |
 usages                     | character varying(255)   |           | not null |
 other_usages               | character varying(100)   |           |          |
 rangleland_entry_id        | integer                  |           | not null |
Indexes:
    "respi_microcatchment_pkey" PRIMARY KEY, btree (id)
    "respi_microcatchment_rangleland_entry_id_2fd812d1" btree (rangleland_entry_id)
Foreign-key constraints:
    "respi_microcatchment_rangleland_entry_id_2fd812d1_fk_respi_ran" FOREIGN KEY (rangleland_entry_id) REFERENCES respi_rangeland_entry(id) DEFERRABLE INITIALLY DEFERRED
Referenced by:
    TABLE "respi_individual_mirocatchment" CONSTRAINT "respi_individual_mir_microcatchment_id_0db1c6d6_fk_respi_mic" FOREIGN KEY (microcatchment_id) REFERENCES respi_microcatchment(id) DEFERRABLE INITIALLY DEFERRED
```

field in migratoin which is refereing to new model name. 

```python
migrations.RenameField(
            model_name='microcatchment_establishment',
            old_name='other_managements_gender',
            new_name='other_who_manages',
        ),

```

solution , add a line in the same migration file but above the lines where migration is renaming fields.  

```python
operations = [  
	migrations.RenameModel('OldModelName', 'NewModelName'),  
	]

or 

        migrations.RenameModel(
            old_name='microcatchment',
            new_name='microcatchment_establishment',
        ),
```


 migrations.RenameModel(