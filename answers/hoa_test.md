require './test/test_helper'
require './lib/owner'
require './lib/building'
require './lib/hoa'

class HomeOwnersAssociationTest < Minitest::Test

  def test_it_exists
    park_lane = HomeOwnersAssociation.new("Park Lane")

    assert_instance_of HomeOwnersAssociation, park_lane
  end

  def test_it_has_a_name
    park_lane = HomeOwnersAssociation.new("Park Lane")

    assert_equal "Park Lane", park_lane.name
  end

  def test_it_starts_without_revenue
    park_lane = HomeOwnersAssociation.new("Park Lane")

    assert_equal 0, park_lane.revenue
  end

  def test_it_starts_without_cash_flow_sheets
    park_lane = HomeOwnersAssociation.new("Park Lane")

    assert_equal [], park_lane.cash_flow_sheets
  end

  def test_it_can_add_cash_flow_sheets
    park_lane = HomeOwnersAssociation.new("Park Lane")
    cf_2018 = CashFlow.new("Cash Flow 2018", "December")
    park_lane.add_cash_flow_sheet(cf_2018)
    cf_2019 = CashFlow.new("Cash Flow 2019", "January")
    park_lane.add_cash_flow_sheet(cf_2019)

    assert_equal [cf_2018, cf_2019], park_lane.cash_flow_sheets
  end

  def test_it_can_calculate_revenue
    park_lane = HomeOwnersAssociation.new("Park Lane")
    cf_2018 = CashFlow.new("Cash Flow 2018", "December")
    park_lane.add_cash_flow_sheet(cf_2018)
    jenn = Owner.new({:name => "Jenn",
                      :unit => 805,
                      :building => "A",
                      :dues => 380})
    cf_2018.add_customer(jenn)

    sharon = Owner.new({:name => "Sharon",
                      :unit => 803,
                      :building => "A",
                      :dues => 420})
    cf_2018.add_customer(sharon)
    cf_2018.collect_dues

    cf_2019 = CashFlow.new("Cash Flow 2019", "January")
    park_lane.add_cash_flow_sheet(cf_2019)

    jenn = Owner.new({:name => "Jenn",
                      :unit => 805,
                      :building => "A",
                      :dues => 380})
    cf_2019.add_customer(jenn)

    sharon = Owner.new({:name => "Sharon",
                      :unit => 803,
                      :building => "A",
                      :dues => 420})
    cf_2019.add_customer(sharon)
    cf_2019.collect_dues

    assert_equal 1600, park_lane.revenue
  end

  def test_it_can_group_by_month
    park_lane = HomeOwnersAssociation.new("Park Lane")
    cf_12_2018 = CashFlow.new("Cash Flow 2018", "December")
    park_lane.add_cash_flow_sheet(cf_12_2018)
    jenn = Owner.new({:name => "Jenn",
                      :unit => 805,
                      :building => "A",
                      :dues => 380})
    cf_12_2018.add_customer(jenn)

    sharon = Owner.new({:name => "Sharon",
                      :unit => 803,
                      :building => "A",
                      :dues => 420})
    cf_12_2018.add_customer(sharon)
    cf_12_2018.collect_dues

    cf_01_2019 = CashFlow.new("Cash Flow 2018", "January")
    park_lane.add_cash_flow_sheet(cf_01_2019)
    jenn = Owner.new({:name => "Jenn",
                      :unit => 805,
                      :building => "A",
                      :dues => 380})
    cf_01_2019.add_customer(jenn)

    sharon = Owner.new({:name => "Sharon",
                      :unit => 803,
                      :building => "A",
                      :dues => 420})
    cf_01_2019.add_customer(sharon)
    cf_01_2019.collect_dues

    expected = ({"December"=> [cf_12_2018],
                "January"=> [cf_01_2019]})
    assert_equal expected, park_lane.group_by_month
  end

  def test_it_can_keep_track_of_monthly_sheets
    park_lane = HomeOwnersAssociation.new("Park Lane")
    cf_12_2018 = CashFlow.new("Cash Flow 2018", "December")
    park_lane.add_cash_flow_sheet(cf_12_2018)
    jenn = Owner.new({:name => "Jenn",
                      :unit => 805,
                      :building => "A",
                      :dues => 380})
    cf_12_2018.add_customer(jenn)

    sharon = Owner.new({:name => "Sharon",
                      :unit => 803,
                      :building => "A",
                      :dues => 420})
    cf_12_2018.add_customer(sharon)
    cf_12_2018.collect_dues

    cf_01_2019 = CashFlow.new("Cash Flow 2018", "January")
    park_lane.add_cash_flow_sheet(cf_01_2019)
    jenn = Owner.new({:name => "Jenn",
                      :unit => 805,
                      :building => "A",
                      :dues => 380})
    cf_01_2019.add_customer(jenn)

    sharon = Owner.new({:name => "Sharon",
                      :unit => 803,
                      :building => "A",
                      :dues => 420})
    cf_01_2019.add_customer(sharon)
    cf_01_2019.collect_dues

    expected = ({"December" => 800,
              "January" => 800})
    assert_equal expected, park_lane.monthly_revenue
  end
end
