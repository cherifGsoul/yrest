# ActiveExportHelper
Yii active record behavior to handle attributes selection and relations selection
## How to use
in the active record class for example Contact

```php
class Contact extends CActiveRecord
{
	......
	public function behaviors(){
		return array(
			'export'=>array(
				'class'=>'ext.yrest.behaviors.models.ActiveExportHelper',
				),
			);
	}

	...
}
```
in the Contact class for example search method

```php
public function search()
{
		// @todo Please modify the following code to remove attributes that should not be searched.

		$criteria=new CDbCriteria;

		$criteria->compare('t.id',$this->id);
		$criteria->compare('firstname',$this->firstname,true);
		$criteria->compare('lastname',$this->lastname,true);
		$criteria->compare('email',$this->email,true);
		$criteria->compare('company_id',$this->company_id);
		$criteria->compare('category_id',$this->category_id);
		$criteria->compare('location_id',$this->location_id);
		$criteria->compare('user_id',$this->user_id);
		$criteria->compare('create_time',$this->create_time);
		$criteria->compare('update_time',$this->update_time);

		return $this->export('t.id,t.lastname,t.firstname',
			array(
				'category'=>array(
					'select'=>'name'
					),
				'company'=>array(
					'select'=>'c.name'
					),
				'location'=>array(
					'select'=>'name'
					)
				),$criteria
			);
	}
```

OR 

```php
Contact::model()->filterScope(''t.id,t.lastname,t.firstname',
			array(
				'category'=>array(
					'select'=>'name'
					),
				'company'=>array(
					'select'=>'c.name'
					),
				'location'=>array(
					'select'=>'name'
					)
				)
			)->findAll($criteria);

Contact::model()->filterScope(''t.id,t.lastname,t.firstname',
			array(
				'category'=>array(
					'select'=>'name'
					),
				'company'=>array(
					'select'=>'c.name'
					),
				'location'=>array(
					'select'=>'name'
					)
				)
			)->find($criteria);

```		

