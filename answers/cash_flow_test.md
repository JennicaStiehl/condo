require './test/test_helper'
require './lib/owner'
require './lib/building'
require './lib/cash_flow'

class CashFlowTest < Minitest::Test

  def test_it_exists
    cf_2108 = CashFlow.new("Cash Flow 2018", "December")

    assert_instance_of CashFlow, cf_2108
  end

  def test_it_has_a_name
    cf_2108 = CashFlow.new("Cash Flow 2018", "December")

    assert_equal "Cash Flow 2018", cf_2108.name
  end

  def test_it_starts_without_cash
    cf_12_2018 = CashFlow.new("Cash Flow 2018", "December")

    assert_equal 0, cf_12_2018.cash
  end

  def test_it_starts_without_customers
    cf_12_2018 = CashFlow.new("Cash Flow 2018", "December")

    assert_equal [], cf_12_2018.customers
  end

  def test_it_can_add_customers
    cf_12_2018 = CashFlow.new("Cash Flow 2018", "December")
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

    assert_equal [jenn, sharon], cf_12_2018.customers
  end

  def test_it_can_collect_customer_dues
    cf_12_2018 = CashFlow.new("Cash Flow 2018", "December")
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


    assert_equal 800, cf_12_2018.cash
  end

  def test_it_has_a_month
    cf_12_2018 = CashFlow.new("Cash Flow 2018", "December")

    assert_equal ("December"), cf_12_2018.month
  end



end
