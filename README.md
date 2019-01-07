# condo

## Iteration 1
### owner
```ruby
pry(main)> require './lib/owner'
=> true
pry(main)> jenn = Owner.new({:name => "Jenn",
                  :unit => 805,
                  :building => "A",
                  :dues => 380})
=> #<Owner:0x007f9079844e30 @building="A", @dues=380, @name="Jenn", @unit=805>
pry(main)> jenn.name
=> "Jenn"
pry(main)> jenn.unit
=> 805
pry(main)> jenn.building
=> "A"

```
## Iteration 2
### building
```ruby
pry(main)> require './lib/owner'
=> true
pry(main)> require './lib/building'
=> true
pry(main)> a = Building.new("A", "480 S Marion")
=> #<Building:0x007f9079856fe0 @address="480 S Marion", @name="A", @owners=[]>
pry(main)> a.name
=> "A"
pry(main)> a.address
=> "480 S Marion"
pry(main)> a.owners
=> []
pry(main)> a.add_owner(jenn)
=> [#<Owner:0x007f9079844e30 @building="A", @dues=380, @name="Jenn", @unit=805>]
pry(main)> sharon = Owner.new({:name => "Sharon",
pry(main)*     :unit => 803,
pry(main)*     :building => "A",
pry(main)*     :dues => 420})
=> #<Owner:0x007f90798d4d00 @building="A", @dues=420, @name="Sharon", @unit=803>
pry(main)> a.add_owner(sharon)

=> [#<Owner:0x007f9079844e30 @building="A", @dues=380, @name="Jenn", @unit=805>,
 #<Owner:0x007f90798d4d00 @building="A", @dues=420, @name="Sharon", @unit=803>
]
```

## Iteration 3
### hoa
Create a class called HomeOwnersAssociation that does the following:
1. collects dues from all customers
2. calculates revenue, year over year
3. can list the revenue from each building
4. can list who has not paid for the previous month
