class HomeOwnersAssociation
  attr_reader   :name,
                :revenue,
                :cash_flow_sheets

  def initialize(name)
    @name = name
    @revenue = 0
    @cash_flow_sheets = []
  end

  def add_cash_flow_sheet(sheet)
    @cash_flow_sheets << sheet
  end

  def revenue
    @cash_flow_sheets.inject(0) do |total, sheet|
      total += sheet.collect_dues
    end
  end

  def group_by_month
    @cash_flow_sheets.group_by do |sheet|
      sheet.month
    end
  end

  def monthly_revenue
    new_hash = Hash.new(0)
    group_by_month.values.each do |sheet|
      group_by_month.keys.each do |month|
        new_hash[month] = sheet[0].cash
      end
    end
    new_hash
  end

end
