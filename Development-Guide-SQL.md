# Development Guide (SQL)

- Don't put single quotes around non string fields:

  ```sql
  42,0
  ```

  not:

  ```sql
  '42','0'
  ```

- No line breaks in the middle of a statement:

  ```sql
  INSERT INTO table_name (a,b,c,x,y,z);
  ```

  not:

  ```sql
  INSERT INTO table_name (a,b,c,
  x,y,z);
  ```

- Spaces in names get replaced with an underscore. Hyphens are allowed. Most other symbols are removed from item/mob/npc names _except_ for polutils_name or packet_name columns, where they must be escaped.
- Full lower case skill/spell/pet/ability things.
- Don't change SQL keywords to lowercase:

  ```sql
  INSERT INTO table_name
  ```

  not:

  ```sql
  insert into table_name
  ```

#### Commenting in SQL

Our SQL tables are big and confusing, and they are also modified by hand. It can be very helpful to leave _short_ comments on your additions and modifications to highlight what they are.

##### Example

Without a comment, this entry is not easily human-readable:

```sql
INSERT INTO `mob_droplist` VALUES (504,0,0,1000,888,340);
```

So we instead store it as:

```sql
INSERT INTO `mob_droplist` VALUES (504,0,0,1000,888,340); -- (Colossal Calamari) seashell
```

Conversely, `Combo` weaponskill doesn't need any additional comments because it has a name field:

```sql
INSERT INTO `weapon_skills` VALUES (1,'combo',0x02020000000200000000000002000000000202000000,1,5,0,16,2000,5,1,8,0,0,0,0);
```

The format of the comment isn't massively important, but it is preferred not to use ';' as a seperator in the middle of your comment. This is a little confusing, as it's the statement-terminator in SQL.

#### Placeholder Data in table rows

In general, it is preferred to comment out the entire row rather than only leaving a comment about still needing to capture it. Examples include item and NPC models. Use your best judgment and if you aren't sure you can always ask.

- If it "works" there is an unfortunate chance nobody will come back to finish it later, including the original author. Life happens, people come and go, take breaks etc.
- If its "wrong" we're likely to still get issue reports on it **because** of that partial implementation, more so than if it were completely missing.
- Experience has shown people don't often read those comments before complaining that "we" got it wrong.
- By having the partial data but commenting it out, it remains obviously incomplete and the next editor can more easily see what needs to happen.
- Example:

```sql
-- Missing model, looks like a fish. Just kidding this doesn't exist and is only a made up example
-- INSERT INTO `item_equipment` VALUES (65534,'holy_moly_mace',43,0,1048645,???,0,0,3,0,0);
```

**_And absolutely never substitute item modifiers!_**

### SQL Migrations for Schema changes

- Going forward schema changes should be accompanied by a migration script.
