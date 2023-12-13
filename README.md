import pandas as pd

file_path = 'homepage_actions.csv'
df = pd.read_csv(file_path)
print(df.head())


duplicate_ids = df[df.duplicated(subset='id')]
print("Duplicate IDs:")
print(duplicate_ids)

viewers_clicked = df[df['action'] == 'click']['id'].nunique()
print("Number of viewers who also clicked:", viewers_clicked)

click_ids = df[df['action'] == 'click']['id']
view_ids = df[df['action'] == 'view']['id'].unique()

click_without_view = df[df['id'].isin(click_ids) & ~df['id'].isin(view_ids)]
print("Clicks without corresponding views:")
print(click_without_view)


control_ids = df[df['group'] == 'control']['id']
experiment_ids = df[df['group'] == 'experiment']['id']
overlap_ids = control_ids[control_ids.isin(experiment_ids)]
print("Overlap between control and experiment groups:")
print(overlap_ids)

# Options include removing overlapping data, stratified sampling, or using statistical methods to control for the overlap.



