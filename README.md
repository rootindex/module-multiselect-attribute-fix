# Magento Multi-select Attribute Indexing Fix

Please note when you run a custom attribute of multiselect & text to be saved on the flat table:

You have to tell the indexer about the flat table column.

```php

public function getFlatColums()
    {
        $attributeCode = $this->getAttribute()->getAttributeCode();
        $column = array(
            'default'   => null,
            'extra'     => null
        );
        if (Mage::helper('core')->useDbCompatibleMode()) {
            $column['type']     = 'varchar(255)';
            $column['is_null']  = true;
        } else {
            $column['type']     = Varien_Db_Ddl_Table::TYPE_VARCHAR;
            $column['nullable'] = true;
            $column['comment']  = $attributeCode . ' column';
        }
        return array($attributeCode => $column);
    }
    
```
