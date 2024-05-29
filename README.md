# Bitrix

## Выборка с пользовательскими свойствами (UF_) раздела в фильтре
```'b_uts_iblock_71_section'
$entity = \Bitrix\Iblock\Model\Section::compileEntityByIblock(71);
$section = (new Query(SectionTable::class))
    ->setFilter([
        '=IBLOCK_ID' => 71,
        '=ACTIVE' => 'Y',
        '!UF.UF_SOME_PROPERTY' => false,
        '=IBLOCK.ACTIVE' => 'Y'
    ])
    ->setSelect(['ID', 'NAME'])
    ->setOrder(['SORT' => 'ASC', 'ID' => 'DESC'])
    ->registerRuntimeField(null, new ReferenceField('UF', $entity, Join::on('this.ID', 'ref.ID')))
    ->registerRuntimeField(null, new ReferenceField('IBLOCK', \Bitrix\Iblock\IblockTable::class, Join::on('this.IBLOCK_ID', 'ref.ID')))
    ->exec()
    ->fetchAll();
```
