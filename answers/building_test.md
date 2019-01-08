require './test/test_helper'
require './lib/owner'
require './lib/building'

class BuildingTest < Minitest::Test

  def test_it_exists
    a = Building.new("A", "480 S Marion")

    assert_instance_of Building, a
  end

  def test_it_has_attributes
    a = Building.new("A", "480 S Marion")

    assert_equal "A", a.name
    assert_equal "480 S Marion", a.address
  end

  def test_it_starts_without_owners
    a = Building.new("A", "480 S Marion")

    assert_equal [], a.owners
  end

  def test_it_can_add_owners
    a = Building.new("A", "480 S Marion")
    jenn = Owner.new({:name => "Jenn",
                      :unit => 805,
                      :building => "A",
                      :dues => 380})
    a.add_owner(jenn)

    sharon = Owner.new({:name => "Sharon",
                      :unit => 803,
                      :building => "A",
                      :dues => 420})
    a.add_owner(sharon)

    assert_equal [jenn, sharon], a.owners
  end

  def test_it_starts_without_revenue
    a = Building.new("A", "480 S Marion")

    assert_equal 0, a.building_revenue
  end

  def test_it_can_calculate_building_revenue
    a = Building.new("A", "480 S Marion")
    jenn = Owner.new({:name => "Jenn",
                      :unit => 805,
                      :building => "A",
                      :dues => 380})
    a.add_owner(jenn)

    sharon = Owner.new({:name => "Sharon",
                      :unit => 803,
                      :building => "A",
                      :dues => 420})
    a.add_owner(sharon)
    a.calculate_building_revenue
    
    assert_equal 800, a.building_revenue
  end
end
