- **Simple Element**: ``<xs:element name=<n> type=<t> />``
	- Contains a simple data type
	- xs:string, xs:decimal, xs:integer, xs:boolean, xs:date, xs:time
- **Attribute** ``<xs:attribute name=<n> type=<t>``
- **simple Type**:Contains only primitive data types
- **complex Type**: Contains other Elements


### Restrictions
```xsd
<xs:element name="car">  
  <xs:simpleType>  
    <xs:restriction base="xs:string">  
      <xs:enumeration value="Audi"/>  
      <xs:enumeration value="Golf"/>  
      <xs:enumeration value="BMW"/>  
    </xs:restriction>  
  </xs:simpleType>  
</xs:element>
```

This can also be written like this:
```xsd
<xs:element name="car" type="carType"/>  
  
<xs:simpleType name="carType">  
  <xs:restriction base="xs:string">  
    <xs:enumeration value="Audi"/>  
    <xs:enumeration value="Golf"/>  
    <xs:enumeration value="BMW"/>  
  </xs:restriction>  
</xs:simpleType>
```


## Sequence
```xsd
<xs:element name="employee">  
  <xs:complexType>  
    <xs:sequence>  
      <xs:element name="firstname" type="xs:string"/>  
      <xs:element name="lastname" type="xs:string"/>  
    </xs:sequence>  
  </xs:complexType>  
</xs:element>
```
Elements firstname and lastname are children of employee