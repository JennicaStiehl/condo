require './test/test_helper'
require './lib/owner'
class OwnerTest < Minitest::Test

  def test_it_exists
    jenn = Owner.new({:name => "Jenn",
                      :unit => 805,
                      :building => "A",
                      :dues => 380})

    assert_instance_of Owner, jenn
  end

  def test_it_has_attributes
    jenn = Owner.new({:name => "Jenn",
                      :unit => 805,
                      :building => "A",
                      :dues => 380})

    assert_equal "Jenn", jenn.name
    assert_equal 805, jenn.unit
    assert_equal "A", jenn.building
  end

end
