# Data Cleaning Agent - Feature Development Plan

## 🔧 Integration Checklist
For each feature implementation, create a to-do list:
1. **File Structure:**
   - [ ] Copy `features/feature_scaffold.ipynb`
   - [ ] Rename to appropriate feature name
   - [ ] Update header documentation
2. **Helper Functions:**
   - [ ] Implement all planned helper functions
   - [ ] Add comprehensive docstrings
   - [ ] Include parameter validation
   - [ ] Add error handling
3. **Main Feature Function:**
   - [ ] Update function name to match feature
   - [ ] Implement LLM routing logic
   - [ ] Add helper function documentation for LLM
   - [ ] Include example usage patterns
4. **Integration:**
   - [ ] Import feature in `route_query.ipynb`
   - [ ] Add to features list with description
   - [ ] Update feature documentation string
   - [ ] Test routing functionality
5. **Testing:**
   - [ ] Test with sample datasets
   - [ ] Verify error handling
   - [ ] Test LLM routing with various queries
   - [ ] Performance testing on larger datasets
6. **Documentation:**
   - [ ] Update README.md with new feature
   - [ ] Include example queries
   - [ ] Document helper functions
   - [ ] Add to capability descriptions
Each feature builds upon the previous ones, creating a comprehensive data cleaning toolkit that maintains the project's modular, LLM-driven architecture.

## 🚀 Quick Win Implementation Features

### 1. Duplicate Detection (`duplicates`)

**File:** `features/duplicates.ipynb`

**Helper Functions:**
- `find_exact_duplicates(df, subset=None)` - Find rows with identical values
- `find_near_duplicates(df, threshold=0.95, subset=None)` - Find similar rows using fuzzy matching
- `remove_duplicates(df, strategy='first', subset=None)` - Remove duplicates with different strategies
- `flag_duplicates(df, subset=None)` - Add boolean column marking duplicates
- `analyze_duplicate_patterns(df, subset=None)` - Show duplicate statistics and patterns

**Implementation Steps:**
1. Copy `feature_scaffold.ipynb` to `features/duplicates.ipynb`
2. Implement exact duplicate detection using pandas `.duplicated()`
3. Implement near-duplicate detection using fuzzy string matching (fuzzywuzzy)
4. Add multiple removal strategies: 'first', 'last', 'most_complete'
5. Create flagging function for inspection before removal
6. Add pattern analysis to show which columns contribute most to duplicates
7. Update main function with LLM routing for natural language queries
8. Add to `route_query.ipynb` imports and features list
9. Test with sample datasets

**Example Queries:**
- "Find duplicate rows"
- "Remove duplicate records keeping the first occurrence"
- "Show me similar records in customer data"

---

### 2. Data Type Optimization (`data_types`)

**File:** `features/data_types.ipynb`

**Helper Functions:**
- `analyze_data_types(df)` - Analyze current types and suggest optimizations
- `optimize_numeric_types(df, downcast='infer')` - Downcast int64→int32, float64→float32
- `parse_dates_auto(df, columns=None)` - Auto-detect and parse date columns
- `convert_percentages(df, columns=None)` - Convert "50%" strings to 0.5 floats
- `categorize_low_cardinality(df, threshold=0.05)` - Convert low-cardinality objects to category
- `detect_boolean_columns(df)` - Find columns that should be boolean
- `memory_usage_comparison(df_before, df_after)` - Show memory savings

**Implementation Steps:**
1. Copy scaffold and rename to `data_types.ipynb`
2. Implement memory analysis function showing current usage
3. Build automatic date parsing with multiple format detection
4. Create percentage string detection and conversion
5. Implement cardinality-based categorization
6. Add boolean detection for Yes/No, True/False, 1/0 patterns
7. Create before/after memory comparison
8. Build comprehensive optimization pipeline
9. Add LLM routing for optimization queries
10. Integrate with route_query system
11. Test memory improvements on large datasets

**Example Queries:**
- "Optimize data types to save memory"
- "Convert date columns automatically"
- "Fix percentage columns"

---

### 3. Outlier Detection & Handling (`outlier_detection`)

**File:** `features/outlier_detection.ipynb`

**Helper Functions:**
- `detect_outliers_iqr(df, columns=None, multiplier=1.5)` - IQR method outlier detection
- `detect_outliers_zscore(df, columns=None, threshold=3)` - Z-score method
- `detect_outliers_isolation_forest(df, columns=None, contamination=0.1)` - ML-based detection
- `visualize_outliers(df, column)` - Create box plots and scatter plots
- `handle_outliers(df, columns=None, method='cap')` - Cap, remove, or transform outliers
- `outlier_summary(df, columns=None)` - Summary of outliers per column

**Implementation Steps:**
1. Copy scaffold to `outlier_detection.ipynb`
2. Implement IQR-based detection (Q1-1.5*IQR, Q3+1.5*IQR)
3. Add Z-score detection for normally distributed data
4. Integrate sklearn IsolationForest for multivariate outliers
5. Create visualization functions using matplotlib
6. Build handling methods: capping, removal, log transformation
7. Add summary statistics for outlier analysis
8. Create comprehensive outlier pipeline
9. Add LLM routing for different detection methods
10. Integrate with existing system
11. Test on various data distributions

**Example Queries:**
- "Find outliers in price column"
- "Remove extreme values using IQR method"
- "Show me outlier patterns in the dataset"

---

### 4. Text Cleaning (`text_processing`)

**File:** `features/text_processing.ipynb`

**Helper Functions:**
- `clean_text_basic(df, columns=None)` - Remove extra whitespace, standardize encoding
- `standardize_case(df, columns=None, case='title')` - Consistent case formatting
- `remove_special_chars(df, columns=None, keep_patterns=[])` - Clean special characters
- `standardize_categorical_values(df, column, mapping_dict=None)` - Map variants to standard values
- `extract_numeric_from_text(df, columns=None)` - Extract numbers from mixed text
- `validate_text_patterns(df, column, pattern)` - Validate against regex patterns

**Implementation Steps:**
1. Copy scaffold to `text_processing.ipynb`
2. Implement basic cleaning: strip, encoding normalization
3. Add case standardization options (upper, lower, title, sentence)
4. Create special character removal with customizable keep-lists
5. Build categorical standardization with fuzzy matching
6. Add numeric extraction from mixed text columns
7. Implement pattern validation using regex
8. Create text quality assessment metrics
9. Build LLM routing for text cleaning tasks
10. Integrate with main system
11. Test with messy real-world text data

**Example Queries:**
- "Clean text columns"
- "Standardize city names"
- "Extract numbers from product codes"

---

### 5. Data Validation (`validation`)

**File:** `features/validation.ipynb`

**Helper Functions:**
- `validate_email_format(series)` - Check email format validity
- `validate_phone_format(series, country_code=None)` - Phone number validation
- `validate_numeric_ranges(df, column, min_val=None, max_val=None)` - Range validation
- `check_data_consistency(df)` - Cross-column consistency checks
- `validate_categorical_values(df, column, allowed_values)` - Check against allowed lists
- `generate_validation_report(df, rules_dict)` - Comprehensive validation report

**Implementation Steps:**
1. Copy scaffold to `validation.ipynb`
2. Implement email validation using regex patterns
3. Add phone number validation with international support
4. Create numeric range validation with boundary checks
5. Build cross-column consistency validation
6. Add categorical value validation against master lists
7. Create comprehensive validation reporting
8. Implement data quality scoring system
9. Add LLM routing for validation queries
10. Integrate with main system
11. Test with various data quality issues

**Example Queries:**
- "Validate email addresses"
- "Check if ages are in reasonable range"
- "Find data quality issues"

---

## 🔮 Advanced Features (Phase 2)

### 6. Feature Engineering (`feature_engineering`)

**File:** `features/feature_engineering.ipynb`

**Helper Functions:**
- `create_bins(df, column, bins=None, labels=None, method='equal_width')` - Create categorical bins
- `create_ratios(df, numerator_col, denominator_col, new_name=None)` - Calculate ratios
- `create_interaction_features(df, col1, col2, operation='multiply')` - Feature interactions
- `create_lag_features(df, column, lags=[1], group_by=None)` - Time series lags
- `create_rolling_features(df, column, window=3, operations=['mean'])` - Rolling statistics
- `create_polynomial_features(df, columns, degree=2)` - Polynomial transformations

**Implementation Steps:**
1. Copy scaffold to `feature_engineering.ipynb`
2. Implement flexible binning with equal-width, equal-frequency, custom methods
3. Add ratio and percentage calculations between columns
4. Create interaction features (multiply, add, divide operations)
5. Build time series lag features with grouping support
6. Add rolling window calculations (mean, sum, std, min, max)
7. Implement polynomial feature generation
8. Create feature importance scoring
9. Add LLM routing for feature creation queries
10. Integrate with main system
11. Test feature engineering pipeline

**Example Queries:**
- "Create age groups in 10-year bins"
- "Calculate price per square foot ratio"
- "Generate interaction features between income and education"

---

### 7. Data Standardization (`standardization`)

**File:** `features/standardization.ipynb`

**Helper Functions:**
- `normalize_columns(df, columns=None, method='minmax')` - Min-max normalization
- `scale_columns(df, columns=None, method='standard')` - Standard/robust scaling
- `encode_categorical(df, columns=None, method='onehot')` - Categorical encoding
- `handle_rare_categories(df, column, threshold=0.01, replace_with='Other')` - Rare category handling
- `create_dummy_variables(df, columns=None, drop_first=True)` - Dummy variable creation

**Implementation Steps:**
1. Copy scaffold to `standardization.ipynb`
2. Implement min-max and z-score normalization
3. Add robust scaling for outlier-resistant standardization
4. Create one-hot, label, and target encoding methods
5. Build rare category consolidation
6. Add dummy variable creation with multicollinearity handling
7. Create standardization pipeline with inverse transforms
8. Add LLM routing for scaling/encoding queries
9. Integrate with main system
10. Test on ML-ready data preparation

**Example Queries:**
- "Normalize numeric columns"
- "One-hot encode categorical variables"
- "Scale features for machine learning"

---

### 8. Export & Formatting Tools (`export_tools`)

**File:** `features/export_tools.ipynb`

**Helper Functions:**
- `export_with_formatting(df, filename, format='csv', options=None)` - Enhanced export options
- `create_data_dictionary(df, filename=None)` - Generate data documentation
- `export_summary_report(df, filename=None)` - Comprehensive data summary
- `format_for_excel(df, filename, sheets=None)` - Excel-optimized export
- `create_codebook(df, filename=None)` - Variable codebook generation

**Implementation Steps:**
1. Copy scaffold to `export_tools.ipynb`
2. Implement enhanced CSV export with encoding options
3. Add Excel export with multiple sheets and formatting
4. Create automatic data dictionary generation
5. Build comprehensive summary reports
6. Add codebook creation for documentation
7. Implement export validation and error handling
8. Add LLM routing for export queries
9. Integrate with main system
10. Test various export scenarios

**Example Queries:**
- "Export to Excel with proper formatting"
- "Create a data dictionary"
- "Generate summary report"

---

### 9. Advanced Data Profiling (`profiling`)

**File:** `features/profiling.ipynb`

**Helper Functions:**
- `generate_profile_report(df, title="Data Profile")` - Comprehensive data profiling
- `calculate_quality_metrics(df)` - Data quality scoring
- `detect_data_drift(df1, df2, columns=None)` - Compare datasets for drift
- `analyze_correlations(df, method='pearson', threshold=0.8)` - Correlation analysis
- `detect_patterns(df, columns=None)` - Pattern detection in data

**Implementation Steps:**
1. Copy scaffold to `profiling.ipynb`
2. Implement comprehensive data profiling with statistics
3. Add data quality metrics and scoring
4. Create data drift detection between datasets
5. Build correlation analysis with visualization
6. Add pattern detection algorithms
7. Create interactive profiling reports
8. Add LLM routing for profiling queries
9. Integrate with main system
10. Test on complex datasets

**Example Queries:**
- "Generate a data profile report"
- "Check for data drift between datasets"
- "Analyze correlations in the data"